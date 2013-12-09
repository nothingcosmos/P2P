put get
###############################################################################

put ::

  //create a peer
  Peer peer = new PeerMaker(new Number160(rnd)).setPorts(port)
              .buildAndListen();

  //store object
  FutureDHT f =peer.put(Number160.createHash(“key”))
               .setObject(“hello world”).start();

  //v5からbuild() -> start() に変わったらしい。

  peer.put(locationkey, domainkey, contentkey, data)
  peer.setData(contentkey, new Data(data))


get ::

  peer.get(nm).start()
  getData().getObject()

ここでいうkeyは、 "key"を160bitのhashに変換して、
160bitのhashに対してobjectをstoreした。

createHash("key")がなかなか曲者かも。

peerのリストは別途管理している。

class Peer
*******************************************************************************

興味深い

Number160 peerId;

DistributedHashTable distributedHashMap
DistributedTracker  distributedTracker
DistributedRouting  distributedRouting


// PutBuilderをかえす。
PutBuilder put(Number160 locationKey) {
  return new PutBuilder(this, locationKey);
}


PutBuilder
===============================================================================

//宣言
class PutBuilder extends DHTBuilder<PutBuilder>

  //private
  Map<Number480, Data> data;
  Map<Number480, Data> dataMap;
  Map<Number160, Data> dataMapConverter;

  super(peer, locationKey);
    self(this);


//objectをsetする。
setObject(xxx).build()  //setObjectは内部でnew Data()してる
setData(xxx).build()

putはEntry単位

Entry<Number480, Data>

setData()

Number160 locationKey
Number160 domainKey
Number160 contentKey

class PutBuilder
  private Entry<Number480, Data> data;
  private Map<Number480, Data> dataMap;
  private Map<Number160, Data> dataMapConvert;

PutBuilder自身をDistributedHashにput(this)する。


DistributedHashTable distributedHashMap
*******************************************************************************
class DistributedHashTable
  DistributedRouting routing
  StorageRPC storeRCP
  DirectDataRPC directDataRPC
  QuitRPC quitRPC

DistributedTracker  distributedTracker
*******************************************************************************
class DistributedTracker
  DistributedRouting routing
  peerBean peerBean
  TrackerRPC trackerRPC
  PeerExchangeRPC peerExchangeRPC
  Random rand

分散Trackerの役割は、他のグループにとのPeerExchange PeerBean

DistributedRouting  distributedRouting
*******************************************************************************
class DstributedRouting

dhtでput/get/add/delete
の際に、routingへ追加する

dhtは、add()とquit()で、routingを作れる。



FutureDHT
*******************************************************************************

StorageRPC
*******************************************************************************

  bloomfilter

  handleGetの際に、bloomfilterをメッセージに載せてかえしている。

FutureRouting
*******************************************************************************


start
*******************************************************************************

patternj.sh "start" | grep public ::

  ./net/tomp2p/p2p/builder/GetTrackerBuilder.java:    public FutureTracker start() {
  ./net/tomp2p/p2p/builder/PutBuilder.java:    public FuturePut start() {
  ./net/tomp2p/p2p/builder/RemoveBuilder.java:    public FutureRemove start() {
  ./net/tomp2p/p2p/builder/DiscoverBuilder.java:    public FutureDiscover start() {
  ./net/tomp2p/p2p/builder/ParallelRequestBuilder.java:    public K start(K futureDHT) {
  ./net/tomp2p/p2p/builder/SendDirectBuilder.java:    public FutureResponse start() {
  ./net/tomp2p/p2p/builder/BroadcastBuilder.java:    public void start() {
  ./net/tomp2p/p2p/builder/AddTrackerBuilder.java:    public FutureTracker start() {
  ./net/tomp2p/p2p/builder/AddBuilder.java:    public FuturePut start() {
  ./net/tomp2p/p2p/builder/DHTBuilder.java:    // public abstract FutureDHT start();
  ./net/tomp2p/p2p/builder/BootstrapBuilder.java:    public FutureBootstrap start() {
  ./net/tomp2p/p2p/builder/PingBuilder.java:    public BaseFuture start() {
  ./net/tomp2p/p2p/builder/GetBuilder.java:    public FutureGet start() {
  ./net/tomp2p/p2p/builder/TrackerBuilder.java:    public abstract FutureTracker start();
  ./net/tomp2p/p2p/builder/SendBuilder.java:    public FutureDirect start() {
  ./net/tomp2p/p2p/builder/ShutdownBuilder.java:    public FutureShutdown start() {


PutBuilderだよな

getDistributedHashTable.put(this)

peerがDistributedHashTable を


parallelrequest でぶん投げる。

isPutIfAbsent

StoreRPC.putifabsent
StoreRPC.put


intermediateっていうステータスがいるのが面白い。
rawDataに毎回putするらしい。

Number160.createHash()
*******************************************************************************
int random
long random
String sha1

最終的にはsha1を作るだけ。



routing
*******************************************************************************

===============================================================================
===============================================================================

template ::
  ###############################################################################
  *******************************************************************************
  ===============================================================================

