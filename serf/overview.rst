serf
###############################################################################
日本語の解説(すごくわかりやすい)
http://masayuki038.github.io/blog/2014/01/13/serf-code-reading/

公式
http://www.serfdom.io/

ベースの論文
"SWIM: Scalable Weakly-consistent Infection-style Process Group Membership Protocol"
http://www.cs.cornell.edu/~asdas/research/dsn02-swim.pdf

特徴
*******************************************************************************
分散システムのクラスタリング部分に焦点を絞ったコンポーネント

クラスタリングをさらに整理し、以下に分割している。

Cluster Membership
  追加、削除(join/leave)

Memberの状態共有
  Failure detection
    ping(probe) //よくあるphi-accrualではない。
    direct probeとindirect probeで、ノードの障害か、routeの障害か見分ける。
  Recovery
    full state syncにより、TCPを使って1:1で状態を共有する。

拡張性
  event handlerの独自拡張と、発火の仕組み


状態の共有方法
  gossip protocol(状態の収斂速度を重視してる?)
  protocolとして、状態共有のためのgossipとFailure detectionのprotocolを分けている。

ノード間の通信方法(3パターン)
probe[1秒]
  UDPでノードの生存をチェックします
full state sync(pushPull)[(ノード数が32までであれば)30秒]
  full state sync(pushPull)はTCPを使い、2つのノード間でお互いが保持するノード情報を同期する。
  join時の情報受け渡しや、定期リカバリ目的でも使用できる。
gossip[200ミリ秒]
  UDP
  broadcast queueを利用して複数のノードに伝搬する。
  compoundMsg
  複数のメッセージをまとめたメッセージ
  pingMsg
  pingメッセージ
  indirectPingMsg
  他ノードを介したpingメッセージ
  ackRespMsg
  pingに対するackのメッセージ
  suspectMsg
  ノードのstateがsuspect(疑わしい)であることを表すメッセージ
  aliveMsg
  ノードのstateがaliveであることを表すメッセージ
  deadMsg
  ノードのstateがdeadであることを表すメッセージ
  userMsg
  ユーザ定義のメッセージ
  compressMsg
  圧縮されたメッセージ


疑問点
*******************************************************************************

===============================================================================
serfはUDPによるgossipと、TCPによる定期リカバリ(full state sync)を組み合わせるのか。。
大変勉強になります。full state syncがあるからseedはいない？


裏書のような収斂を支援する仕組みはあるか

===============================================================================
===============================================================================
===============================================================================
===============================================================================
===============================================================================


