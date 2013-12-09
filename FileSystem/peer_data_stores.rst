
Distributed_data_store
###############################################################################

http://en.wikipedia.org/wiki/Distributed_data_store

Distributed non-relational databases

* Apache Cassandra, former data store of Facebook
* BigTable, the data store of Google
* Dynamo of Amazon
* HBase, current data store of Facebook's Messaging Platform
* Riak
* Voldemort, data store used by LinkedIn

Peer network node data stores

* BitTorrent
* Chord project (DHT)
* GNUnet
* Freenet
* NNTP (the distributed data storage protocol used for Usenet news)
* Mnet
* Storage@home
* Tahoe-LAFS

BitTorrent
*******************************************************************************

* Throttling and encryption

Main article: BitTorrent protocol encryption

PHE and MSE/PE(Message stream encryption/Protocol encryption)

* Decentralized keyword search

Tribler http://en.wikipedia.org/wiki/Tribler

peer or index sites. add gossip protocol

Cornell University
peer to peer network for inexact strings

gossip protocolに関して
*******************************************************************************
http://www.dsl.mei.titech.ac.jp/research/2011/ishikawa/

gossip protocol はfloodingの欠点を改善する。
ネットワークの帯域を圧迫する。

floodingはロバスト性があるが、gossipはどうか。


Dynamoはgossipベースの分散障害見地とメンバーシッププロトコル

メンバーシップ変更を伝搬させるために使用する。
パーティショニングと配置の情報の伝搬にも使用する。

Tahoe-LAFS(Tahoe Least-Authority Filesystem)
*******************************************************************************

v1.10.0 released

GPUv2

secure, decentralized, fault-tolerant,
peer-to-peer distributed data store and distributed file system.

* 資料
http://www.snia.org/sites/default/files2/SDC2012/presentations/File_Systems/PhillipClark_A-Case_Study_Object_Storage.pdf
http://www.youtube.com/watch?v=SCgl0xXFVOg

* 分散ファイルシステムの仲間

* GlusterFS
* XtreemFS
* iFolder
* Coda (file system)
* Freenet
* Lustre (file system)
* Ceph (file system)
* Parallel Virtual File System
* List of distributed file systems
  * Ceph
  * FhGFS
  * GlusterFS
  * Quantcast File System-QFS
  * Lustre
  * OpenAFS
  * Tahoe-LAFS
  * HDFS
  * Amazon S3
  * Google Cloud Storage
  * SWIFT(OpenStack, Rackspace)
  * Microsoft Azure
  * Cleversafe
* Comparison of distributed file systems

FUSEがメジャーなのか。



* ぐぐった情報

暗号化して他者から見えないようにする。セキュア
pythonで開発され、FUSE(file system in userspace)

IIJ(TAMIAS project)
http://www.iij-ii.co.jp/techweek/2011_03.html

Tahoe-LAFSには、データ共有の管理機能やユーザ管理機能がない。
セキュアストレージの基本機能はTahoe-LAFS

S4 service


TAMIAS
*******************************************************************************
https://tamias.iijlab.net/

GPLv3

opensource & privacy-aware distributed storage system


* 資料

https://tamias.iijlab.net/wp-content/uploads/2011/04/20110419_tamias_report_cristel.pdf

https://tamias.iijlab.net/wp-content/uploads/2011/04/poster_fast11.pdf

https://tamias.iijlab.net/wp-content/uploads/2011/08/20110726_tamias_fedAndnotif.pdf




TomP2P
*******************************************************************************
http://tomp2p.net/

Dr. Thomas Bocek さんを中心に開発しているらしい。

http://www.csg.uzh.ch/staff/bocek.html

TomP2P is an advanced DHT, which stores multiple values for a key.
Each peer has a table (either disk-based or memory-based) to store its values.
A single value can be queried / updated with a secondary key.
The underlying communication framework uses Java NIO to handle many concurrent connections.

keyword and slide
===============================================================================

* Keywords

Overlay Network, Peer-to-Peer (P2P), Distributed Hash Table (DHT), Java DHT implementation, Kademlia

* Feature

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


* slide

http://www.csg.uzh.ch/teaching/fs12/p2p/lectures.html
http://tomp2p.net/doc/P2P-with-TomP2P-1.pdf
http://tomp2p.net/doc/P2P-with-TomP2P-2.pdf

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

Overlay Weaver

FreePastry


TomP2Pが使用しているライブラリ
===============================================================================
Apache MINA -> Netty


TODO
===============================================================================

tomp2p 5
next versionを開発中で、featureが挙がっている。

http://tomp2p.net/dev/tomp2p_5/

TomP2Pでは、Friendly Shutdownが課題になっているらしい。興味深い

BitCoin
*******************************************************************************

===============================================================================
===============================================================================

tahoe-lafs Other projects
*******************************************************************************

These projects have no specific relationship with our project,
but they are similar in some ways and so may be of interest.

We sometimes exchange ideas with the developers of some of these projects,
especially on the p2p-hackers mailing list.

* bup
  is a backup tool with "convergent variable-length block deduplication".
  It re-uses some of git's internals. featured in Tahoe-LAFS Weekly News issue 9;
  licence: GPLv2

* backshift
  is a backup tool with "convergent variable-length block deduplication",
  as well as compression and incremental updates. written in Python;
  licence: GPLv3

* HekaFS is a project to add encryption and other multi-tenancy features to Gluster filesystem.
  It is sponsored by RedHat, who recently bought Gluster;
  featured in Tahoe-LAFS Weekly News issue 14;
  licence: GPLv3

* Ugarit
  is a storage system inspired by Venti and implemented in Chicken Scheme.
  Immature—it currently can't use a remote backend, only a local POSIX filesystem.
  licence: BSD

* GNUnet
  is an anonymous, censorship-resistant, file-sharing network.
  licence: GPLv2+

* Camlistore
  is a distributed data store plus some ideas about synchronization, sharing, and modelling.
  licence: Apache

* git
  is a decentralized revision control tool.
  No wait!
  It is a beautiful decentralized data store with a grotesque revision control tool built on top.
  (Zooko takes full responsibility for this careless slander.)
  licence: GPLv2

* FreeNet
  is a long-running project to make a decentralized and censorship-resistant file-sharing network.
  featured in Tahoe-LAFS Weekly News issue 7, FAQ in FAQ 1.5;
  licence: GPLv2

* Firefox Sync
  (originally named "Weave") is a project to securely share your web browser metadata such as cookies,
  saved passwords, and bookmarks. Comes standard in Firefox.
  licence: Mozilla

* Octavia
  is a new distributed filesystem inspired by Tahoe-LAFS
  and intended to improve on Tahoe-LAFS in performance and usability.
  It is very new and not yet usable except for experimentation.
  licence: GPL

* Nilestore
  is a secure and fault tolerant distributed storage system built
  using Kompics component model framework following the design of Tahoe-LAFS.
  currently it implements the immutable file upload and download.
  featured in Tahoe-LAFS Weekly News issue 11;
  licence: GPLv2

Variable-Length Deduplication
===============================================================================

可変長ブロックの重複排除は、固定長の場合と比べたメリットとして、

ストリームが途中から全部ずれた場合なんかに効果がある。

可変長ブロックの場合、特定の範囲の冗長性を検出する。

可変長で重複排除するため、場合によってはアンカーを設置して複数の参照を持ちうる

http://www.emc.com/corporate/glossary/variable-length-deduplication.htm


