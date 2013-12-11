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

Create a cooperative peer to peer distributed network not only to stora file data, but also to be able to communicate, creating a trust-based peer-to-peer social network, that can be used to distribute anything, from streaming media to messaging, services (running processes), and entire directory structures. Encryption will be mandatory, no exception. Data stored on disk will be encrypted using strong block-encryption methods (like GPG), and communications will be encrypted using strong streaming encryption methods (like RSA), with connections multiplexed to several encrypted streams with different keys (and possibly different encryption protocols), each stream's keys will be changed frequently through a different stream. This is so that even if a stream is stored in it's entirety, and one key cracked, the attacker has only acces to a small portion of the communication that has no meaning in itself. We know of the overhead of this encryption scheme, but we argue that since most bandwidth and cpu power is wasted anyways, it's not really a big issue.

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

  * Block encryption using GPG
  * stream encryption using RSA (maybe mixing RSA with others in parallel streams)

Distribution
------------
  * Currently the most advanced technology peer to peer lookups is a DHT, there are several candidates as to which type of DHT should be used
    * Kademlia is the most widely used DHT
    * Chord has better characteristics on paper, but seems to be more complicated to implement
    * the method freenet (new version) uses also looks promising
  * Data distribution: a modified version of the bittorrent protocol should work, wich allows for changing data inside a torrent

I really like the idea that plan9 used with Venti and Fossil. Venti is a block store, and fossil is a filesystem that builds on that. I would go further with the idea:
  * A permanent block store for each user's own data
  * a worm cache, that can use unused disk space to cache other user's data, and can simply be garbage collected by discarding the least used blocks

In this scheme, when a user accesses an other user's data, the blocks are cached to his disk, creating multiple redundant and local copies of the blocks of each user's files.

Streams should just be streams of block's hashes, which can then be fetched from the DHT.

Duplication of effort?
======================

I do not think I am duplicating the effort of any network. The closest one to my goal is the freenet project, but since it is written in java, it is very inefficient.
