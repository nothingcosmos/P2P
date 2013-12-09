TomP2P
===============================================================================
http://tomp2p.net/

https://github.com/tomp2p/TomP2P

Dr. Thomas Bocek さんを中心に開発しているP2P型のDHT

http://www.csg.uzh.ch/staff/bocek.html

TomP2P is an advanced DHT, which stores multiple values for a key.
Each peer has a table (either disk-based or memory-based) to store its values.

A single value can be queried / updated with a secondary key.
The underlying communication framework uses Java NIO
to handle many concurrent connections.

keyword and slide
===============================================================================

* Keywords

Overlay Network, Peer-to-Peer (P2P), Distributed Hash Table (DHT),
Java DHT implementation, Kademlia

* Slide

http://www.csg.uzh.ch/teaching/fs12/p2p/lectures.html (講義資料は学内からしか参照できないらしい。)
http://tomp2p.net/doc/P2P-with-TomP2P-1.pdf
http://tomp2p.net/doc/P2P-with-TomP2P-2.pdf
http://www.csg.uzh.ch/staff/hecht/publications/btracker-cr.pdf
http://tomp2p.net/downloads/M06-6up.pdf

* B-Tracker

DHT
Peer Excahnge(PEX, PeX) これは定期実行。every minitu push
B-Trackerがmesh,load balancing

Vuzeでテスト中


Feature
*******************************************************************************

* Java6 DHT implementation with non-blocking IO.
* XOR-based iterative routing similar to Kademlia.
* Standard DHT operations: put, get
* Extended DHT operations and support for custom operations
* Direct and indirect replication.
* Mesh-based distributed tracker.
* Data protection based on signatures.
* Port forwarding detection and configuration via UPNP.
* Runs with IPv6 (tested with Linux) and IPv4.
* Network operations support the listenable future objects concept.
* Scales up to 2160 peers (more than you can address with IPv6)

TomP2Pが使用しているライブラリ
===============================================================================

Apache MINA -> Netty


TomP2Pを使用しているアプリケーションの一覧
===============================================================================

* LiveShift

http://www.csg.uzh.ch/research/liveshift.html

Live Video Streaming

* DRFS
* P2PFastSS
* PeerVote
* PSH/CompactPSH
* P2P-PTT, a P2PSIP based PTT service
* EC-GIN (Europe-China Grid InterNetworking)

* Similar Projects

Overlay Weaver, FreePastry

Code Examples (API version 4.1) ::

  //create a peer
  Peer peer = new PeerMaker(new Number160(rnd)).setPorts(port).buildAndListen();
  //store object
  FutureDHT f =peer.put(Number160.createHash(“key”)).setObject(“hello world”).build();
  //get object
  FutureDHT f = peer.get(Number160.createHash(“key”)).build();
  //to get the result, either add listener
  f.addListener(...)
  //or block
  f.await()
  //send direct messages to a particular peer
  peer.sendDirect().setPeerAddress(peer1).setObject(“test”).build();


template ::
  ###############################################################################
  *******************************************************************************
  ===============================================================================

