bloomfilter
###############################################################################

B-TrackerではBloomFilterを使用しているらしい。

Applications: Distributed Caching, Spell checking, Routing, (distributed) Databases

B-Tracker uses Bloom Filters
M06, slide 22 “To avoid duplicates send compressed list of known peers”
Idea: store peers in Bloom Filter and send it.
Other peers only send us peer not in the Bloom Filter
 Less traffic (request is larger, reply may be smaller)
 False positive are possible

BloomFilterのPeer に対して、storeかつBloomFilterを送付する。
他のPeerはBloomFilterを送付するのみ。BloomFilterにないものは。

TrackerがBloomFilter

SimpleBloomFilter
*******************************************************************************
どれもPeer160をtrackする。

AddTracker
  bloomFilter knownかどうかの判定

GetBuilder
  keyBloomFilter
  contentBloomFilter

RoutingBuilder
  keyBloomFilter
  contentBloomFilter

Digestがたくさんもってる。


上記のメンバに定義されている。


どちらもmessageでやりとりするらしい。
ただし、メッセージングするBloomFilterはリスト構造になってるっぽい。
追い難い。全部そこにpushする。

GetHandleが面白い。
domain location contents key をmessagingする

getでbloomfilterを中間要素として返して、jjj



*******************************************************************************
近傍探索(search)の際に、複数の要素(searchValue)をBloomFilterで返す。


AddTrackerでは、known peerをBloomFilterでメッセージングする。
meshpeers も関係ある。で探せば見つかるかも。
tracker peerのbloomfilterknownをやりとりする。


===============================================================================


message type
===============================================================================

        // REQUEST_1 is the normal request
        // REQUEST_2 for GET returns the extended digest (hashes of all stored
        // data)
        // REQUEST_3 for GET returns a Bloom filter
        // REQUEST_4 for GET returns a range (min/max)
        // REQUEST_2 for PUT/ADD/COMPARE_PUT means protect domain
        // REQUEST_3 for PUT means put if absent
        // REQUEST_3 for COMPARE_PUT means partial (partial means that put those
        // data that match compare, ignore others)
        // REQUEST_4 for PUT means protect domain and put if absent
        // REQUEST_4 for COMPARE_PUT means partial and protect domain
        // REQUEST_2 for REMOVE means send back results
        // REQUEST_2 for RAW_DATA means serialize object
        // *** NEIGHBORS has four different cases
        // REQUEST_1 for NEIGHBORS means check for put (no digest) for tracker
        // and storage
        // REQUEST_2 for NEIGHBORS means check for get (with digest) for storage
        // REQUEST_3 for NEIGHBORS means check for get (with digest) for tracker
        // REQUEST_4 for NEIGHBORS means check for put (with digest) for task
        // REQUEST_FF_1 for PEX means fire and forget, coming from mesh
        // REQUEST_FF_1 for PEX means fire and forget, coming from primary
        // REQUEST_1 for TASK is submit new task
        // REQUEST_2 for TASK is status
        // REQUEST_3 for TASK is send back result

template ::
  ###############################################################################
  *******************************************************************************
  ===============================================================================

