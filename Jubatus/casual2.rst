jubatus casual #2
================================================================================

処理性能とデータ量が大事なんだよ

ルールベースではない。

教師あり学習

オンラインで高速に学習できる。
分散環境とmix

データを解析したら捨てるモデル

並列処理できる。mixが特徴。

jubatusの開発
================================================================================
開発方法の紹介

suma-san

0.5 release

保存モデルのデータフォーマットを規定

jubakeeperからjubaproxyへ名称変更

jubatusの今後の課題

RPC の限界。。
タイムアウト等。。
耐障害性の構造
1プロセスで一つのモデルを実行しているが、今後はどうするか。。

異常検知入門
================================================================================

異常検知の基本的な仕組み

異常検知の代表3つ

外れ値問題
変化が起きたかどうか。変換点検出
異常かどうか判定

jubatusではlofを実装している。

他の方法は次元の呪いがあって困ってしまう。高次元だと困ってしまう。
lofは次元が高くなってもちゃんと動くのが特徴。

これが高速
sugiyama borgwardt NIPS2013

4個検出して、その中心を計算して、距離を計算して、はずれたのが異常値。
単純な方法だけど、正しくことの証明付き。
Rapid Distance-Based Outlier Detection via Sampling

異常検知の処理は、以下の2つの処理を利用することが多い。
平均と標準計算
その統計計算


//以下ソースコードリーディング

anomaly scoreを計算して返す？

anomalyパッケージがメインで、
そこにlofとlight lofが定義されている。
依存パッケージは nearest_neighbor と recommander

"lof"は Local Outlier Factor [Breunig2000]

"lof"   Recommenderベースのlofと、
"light_lof"   Nearest Neighborベースが利用できる。

依存するstorageは、
storage lsh
lof storage

lsh function(neighborのパラメータ) Locality Sensitive Hashing


異常値検出の冗長化、底レイテンシ化のためのアーキテクチャに関して
================================================================================
データのみ分散化しても実現するのは難しい。


ある程度の前処理が行われている。
mixしているのか？

ベースはneighberと なので、こちらのmix化可能かに依存する。


時系列解析
================================================================================

移動平均みたいなものか。
これは時系列ごとにそーとが必要か。

Storm/Kafka
================================================================================

リアルタイム向け

秒間1万データ。jubatus

エラーのラベルがついたセンサーデータ
無印のラベルがついてる。
センサーデータのリアルタイム分析しながら切り分けたい。


apache kafka raddit mq
jubatus samoa
データの可視化

kafka
================================================================================
高速らしい。linkedin
publisher-subscibeモデル
storm by twitter streamをspout/boltに繋いで処理をっ記述するフレームワーク


死活や際木津緒もあり。耐障害性がある。
メッセージの処理保証とトランザクションもサポートしている。

SAMOA yahoo ストリームデータの分散機会学習。下回りはS3なども下回り差し替え可能。
0.0.1らしいよ。


データ生成はシミュレーション

kafka -> storm/jubatus

stormのトポロジにjubatusをbundle
kafkaで分類。

storm - jubakeeperを同居させている。普通にjava rpcでながしている。入力はある程度サンプリング
データを10000/secまで増やして並列度を試してみた。 可視化までしてみる。

10000件/secを実現できた。
ノードの並列度は、kafka4 jubatus 8
storm 分類処理がボトルネックだったかも

storm 並列数
kafka
振り分け
分類  ここは1mくらいの遅延になる。rpcなので。600-700が限界になっていた。
TODO javaのrpcが遅いのでは説。c++ rpc(空)は9000/secが出たとblogに記述があるらしい。


kafkaは10000件くらいまで余裕でいけた。


全体のスループットの変化を観ると、mixerの際にがっくり落ちているように見える。
jubaproxyの数が増えていくと、zookeeperとの通信でtimeoutが発生したりしていた。


異常値検出やラベル付けはなにをつかってたんだろうね。
ちらっと紹介していたけど忘れた。


分散処理の方法
================================================================================
ゆるくモデルを共有して分散処理している。

それぞれが個別に学習する。
たまにNodeが勉強会を開いて、情報交換する。

そのため、基本的にはローカルでシステムが動いている。

サーバの参加、離脱がおおいと、mixでどんどん精度が悪化していく問題

また、レイテンシとスループットがあり、レイテンシはアルゴリズムで実現する。
分散によりスループットの上昇を目指す。


分散に関して
********************************************************************************

分散に関して
================================================================================
勉強会を開く仕組みと
障害検知くらいは
モデル情報の共有方法


jubatusのAPI
================================================================================

classifierのAPIを元に解析する

jsonでデータ構造を与える。
idlで構造を定義している。

jsonでデータをpushする際に、引数等を指定できる。

methodで処理を指定する。

method単位で引数はことなる。

dataを指定したり

jsonのデータへのconverterが用意されている。

結果もdataでもらえる。

まとめ
================================================================================
内部のAPIは恐らく固定

jsonを利用
idlで指定

外部のAPIはidlごとに説明している。


