TODO
###############################################################################

tomp2p v5
next versionを開発中で、featureが挙がっている。

http://tomp2p.net/dev/tomp2p_5/

TomP2Pでは、Friendly Shutdownが課題になっているらしい。興味深い

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

BTracker
*******************************************************************************

詳細は？

mesh状に分散 ???

Primary, Secondary???

DistHashとDistRoutingとDistDataEntryがあったけど、どれ

データ配置の分布は一様にはならないけれども、ネットワークを占める転送量がDHTよりも少なくなる？

update
*******************************************************************************

primary と secondary Trackerのみ

addAsProvider

delete
*******************************************************************************

primary と secondary Trackerのみ

removeAsProvider

バックグラウンド処理は
*******************************************************************************

coupon collector

bloom filter

 ::
  ###############################################################################
  *******************************************************************************
  ===============================================================================

