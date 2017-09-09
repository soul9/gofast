gofast
======

gofast censorship fighting peer to peer network

Goal
======

The goal of this network is to replace current internet infrastructure with a truly distributed network.

Issues with the current infrastructure
======================================

The current internet infrastructure has several weaknesses:

  * Being based on trust, it has not been able to cope with it's massive growth
  * Having no strong encryption and identification, it's vulnerable to spam attacks
    * Fighting spam induces more complexity, and is very inefficient in fighting spam
  * Hundreds of milions of devices' computing power, bandwidth and storage capacity are mostly wasted
  * Governments and agencies can snoop users' communication and tap into their data too easily
  * We are still stuck in the "mainframe" computing, where there are big machines, hosted in special places,  and terminals that connect to them

Solutions
=========

Create a cooperative peer to peer distributed network not only to stora file data, but also to be able to communicate, creating a trust-based peer-to-peer social network, that can be used to distribute anything, from streaming media to messaging, services (running processes), and entire directory structures. Encryption will be mandatory, no exception. Data stored on disk will be encrypted using strong data at rest encryption methods (like [DARE](https://github.com/minio/sio/blob/master/DARE.md)), and communications will be encrypted using strong streaming encryption methods (like TLS) with connections multiplexed to several encrypted streams with different keys (and possibly different encryption protocols), each stream's keys will be changed frequently through a different stream. This is so that even if a stream is stored in it's entirety, and one key cracked, the attacker has only acces to a small portion of the communication that has no meaning in itself. We know of the overhead of this encryption scheme, but we argue that since most bandwidth and cpu power currently is wasted anyways, it's not really a big issue since less resources should be wasted on the whole with this new scheme.

The goal is to replace the following protocols among others:
  * SMTP
  * HTTP
  * DNS
  * XMPP
  * skype
  * rsync

Technical decisions
===================

I have chosen GO as the language I wish to implement the system in for a couple of reasons:
  * It has found a  sweet-spot with regards to programming complexity and speed
  * It has a good concurrency scheme built-in
  * Gophers

Encryption
----------

  * Block encryption using the DARE format ( https://github.com/minio/sio/blob/master/DARE.md )
  * stream encryption using RSA (maybe mixing RSA with others in parallel streams)

Distribution
------------
  * Currently the most advanced technology for peer to peer lookups is a DHT, there are several candidates as to which type of DHT should be used
    * Kademlia is the most widely used DHT
    * Chord has better characteristics on paper, but seems to be more complicated to implement
    * the method freenet (new version) uses also looks promising
  * Data distribution: a modified version of the bittorrent protocol should work, wich allows for changing data inside a torrent

I really like the idea that plan9 used with Venti and Fossil. Venti is a block store, and fossil is a filesystem that builds on that. I would go further with the idea:
  * A permanent block store for each user's own data
  * a hit-counted cache, that can use unused disk space to cache other user's data, and can simply be garbage collected by discarding the least used blocks

In this scheme, when a user accesses an other user's data, the blocks are cached to his disk, creating multiple redundant and local copies of the blocks of each user's files. This would allow most used data on a specific device to still be available offline.

Streams should just be streams of block's hashes, which can then be fetched from the DHT.

Features
========

# redundancy

a redundency level should be specifyable for every directory/file. This would then try to make sure the data is stored on at least that many computers at all times. this will be difficult to implement, especially if there is a lot of churn. See resource acquisition

# Resource acquisition

A blockchain-like system for making resources available to other people, based on scarcity, should be used. A way to securely store data on untrusted machines and securely execute code on untrusted machines should be implemented. This could either work on a social-network base: I trust people and optionally implicitly trust the people they trust, or on verification basis: if I store data on a machine, can I retrieve the same data? if I execute some code on a machine are the results the same as when executed on an already trusted machine? The main resources I can see is CPU time, data storage and network bandwidth

# sync

once data is written and flushed, all devices should see the same data right away (and RAID sync start, etc)

Duplication of effort?
======================

I do not think I am duplicating the effort of any network. The closest one to my goal is the freenet project, but since it is written in java, it is very inefficient.

IPFS: while many of the goals are the same, ipfs is read-only. I want to be able to access all my files from any of my computers.
