jubatus source code reading
================================================================================

分散処理ののりかた
================================================================================

jubatus/server/serverに、各処理のimplやserverが乗っている。

================================================================================
================================================================================


分散処理の通信部分
================================================================================

jubatus/server
================================================================================

membershipとかcommonに入っている。

lock serviceとかk


server
  start
  join
  dispatch reqのinvoke

  void listen(uint16_t port);
  void listen(uint16_t port, const std::string& bind_address);
  void start(int nthreads, bool no_hang = false);
  void join();
  void end();
  void stop();
  void close();

server/commonがおもしろいかもね。
zoo_wgetで実行



cache系はread/cache/list/reload

cht consistent hashing が含まれている。

ipとportのpairをfind_predecessorで検出
chtディレクトリを作成する。これはローカル？zkを使って

zk使ってファイルを作っている。
ディレクトリの産むでatomicに操作

lockはzk巻かせ。lock service

lsはlock_service


zkmutex
try_locable

createもします。。

zk経由でlock/create filepathでユニークを取っている。
membershipは、


create_lock_service()
zkだったらzkを作るだけ。builderパターン



zkには、
lockとmembershipまかせ。
障害児には、listとlockの産むだけでもんだいなし
mixerでゆるふわ分散なので問題なさそう。


jubavisor
================================================================================
mainがある。完全に別のプログラム

rpc port, zookeeper port, deamon 

rpc_join


process

ローカルのプロセスを管理する。そのためsignal handlerを用意している。
そのserverっ機能が存在すると。
ローカルに複数プロセスを起動し、複数を管理するproxyと、その実態のprocess 待ち受けようのserver

start/stop
  spawn_link
    redirect
      /dev/null

fv_converter
================================================================================

fvは特徴ベクトルの略ね。

idl連携のデータ変換かな。

入力データと保存データの形式を定義し、いろいろ変換していそう。。


dynamic_loaderがいて、dlopenできるらしい。。
pluginしてデータ変換を外部モジュールを読み込んで動的に実行できる。

pluginのパスを指定して、dlopenして実行できる。


ストレージ部分の設計
================================================================================
jubatus/core/storage

local storage

kvsになっている。keyは基本的にはstringかな。
msgpackでserialize前提になっている。
pack/unpackとかそういうの。

storage_baseを読むのがいいの

mixture専用のストレージが定義されてる


lsh storageってのがでかいかも

normっっていうデータ構造がstorageにある


TODO
================================================================================

検索はどうなっている

mecabかな？



