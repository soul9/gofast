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

Create a cooperative peer to peer distributed network not only to stora file data, but also to be able to communicate, creating a trust-based peer-to-peer social network, that can be used to distribute anything, from streaming media to messaging, and entire directory structures. Encryption will be mandatory, no exception. Data stored on disk will be encrypted using strong block-encryption methods (like GPG), and communications will be encrypted using strong streaming encryption methods (like RSA), with connections multiplexed to several encrypted streams with different keys (and possibly different encryption protocols), each stream's keys will be changed frequently through a different stream. This is so that even if a stream is stored in it's entirety, and one key cracked, the attacker has only acces to a small portion of the communication that has no meaning in itself. We know of the overhead of this encryption scheme, but we argue that since most bandwidth and cpu power is wasted anyways, it's not really a big issue.

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
  * It has founda  sweet-spot with regards to programming complexity and speed
  * It has a good concurrency scheme built-in
  * Gophers

