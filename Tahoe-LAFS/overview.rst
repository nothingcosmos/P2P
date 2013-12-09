tahoe-lafs
###############################################################################
License GPLv2

pythonで作成された暗号化された分散ファイルシステム。セキュリティ重視なのが特徴。

key-value storeおよびネットワークの下回りがp2pらしい。

開発はpython + FUSE(filesystem in userspace)

https://tahoe-lafs.org/trac/tahoe-lafs/wiki/RelatedProjects
===============================================================================

pythonのライブラリをいくつかリリースしている。

#zfec erasure-codes(Reed-Solomon Coding)のライブラリ。 GPLv2
#pycryptopp tahoeの内部で使用している暗号化ライブラリ。GPLv2

https://tahoe-lafs.org/trac/tahoe-lafs/wiki/Doc
*******************************************************************************

reading docs

three layer
*******************************************************************************

top    : application
middle : filesystem
lowest : key-value store

key-value store
===============================================================================

valuesはsequences byte data

dataはencrypted and destributed

valueにsizeはない。

storageはuser-space processes

TCP over

encoded pieces , 10 normally pieces

bi-clique topology
完全2部グラフ


other nodes behind NAT boxes


* introducer の役割
Single Point of Failure, SPoF
future release, decentrized introducer

hostname, private key

grid topology

* File Encoding

secure hashes, Merkle Trees

client は erasure-codes を各セグメントにかける。 3/10 デフォルト

encryptionのhashは、"storage index"に存在する。

erasure-decoding

* Capabilities

modeを入力データのbitに依存し、複数のモードを持つ。
切り替えタイミングは？複合的に使用できるのか？

read-only  mutable filesを複数versionのfileで管理する。

read-write writeはnew versionへの書き込みとなる。

location と identification

self-authenticating

server selection
===============================================================================

introducer にファイルのありかを問い合わせる

2*N elements のpermuted listを管理する。

* future work

large ring, Chord routing

small node(100) -> permuted hash list



filesystem
===============================================================================

decentralized filesystem

directed graph

directories and leaf node are files

no metadata

pathnames,

filesystemは2つのcapabilityを持つ。read-write read-only

read-onlyのファイルは、read-writeからは参照不可能。

* Leases, refreshing, Garbage Collection

GCを用意。space-reclamation process





application
===============================================================================

backup service

copy local disk to decentralized filesystem


*******************************************************************************
*******************************************************************************

===============================================================================
===============================================================================

Tahoe Storage Illustration
*******************************************************************************
http://bigasterisk.com/tahoe-playground/

1. Enter plaintext
hello world

2. Encrypt
Generated URL for this file :
http://localhost:8123/uri/URI%3ACHK%3Ardr56qlouz2mlx4gf7l4xgh5nf:o6fgjq6un52hlwaccyiqy4hmmwl4ghjzdbvoifwjysns5vizrz42:3:10:11
Complete, encrypted data: 暗号化済み
arjen2wmthalb764we76d24igjndkqxm7mnof25yt5lug737hxtzd

3. Store
10個に分散してデータを格納

4. Recover
1,2,3からデータを復元

3/10存在していれば復元可能だが、3より少なくなると復元できない。

erasure codesの成果っぽい。
再構築時間をなるべく短くできるのが利点

RAID-6はerasure coding
http://en.wikipedia.org/wiki/Erasure_code


reliable系はこちらが詳しいかも。
http://www.cs.umd.edu/class/spring2007/cmsc818s/Lectures/erasure.pdf




===============================================================================
===============================================================================



memo
*******************************************************************************

v1.10.0 released

GPUv2

secure, decentralized, fault-tolerant,
peer-to-peer distributed data store and distributed file system.

アーキテクチャの概要だけみると、
Tahoe-LAFS gatewayのクライアントに集約されているような。。

RAIN(Reliable array of independent nodes)

Principle of least privilege

Zooko Wilcox-O'Hearn
http://en.wikipedia.org/wiki/Zooko_Wilcox-O%27Hearn

分散ファイルシステムの仲間

* GlusterFS
* XtreemFS
* iFolder
* Coda (file system)
* Freenet
* Lustre (file system)
* Ceph (file system)
* Parallel Virtual File System
* List of distributed file systems
* Comparison of distributed file systems


関連プロジェクト
*******************************************************************************

S4
===============================================================================
Tahoe-LAFS

をバックエンドに使用した、セキュアなストレージサービス


資料
*******************************************************************************
http://www.youtube.com/watch?v=SCgl0xXFVOg

http://www.snia.org/sites/default/files2/SDC2012/presentations/File_Systems/PhillipClark_A-Case_Study_Object_Storage.pdf

http://eprint.iacr.org/2012/524.pdf

http://www.lexort.com/blog/tahoe-lafs.htm

===============================================================================

securityはprovider-independent
clientでEncryption/Decryption
Storage Nodeには暗号化されたまま格納されている？
partial and encrypted

Client/Gatewayが存在する。
Introducerが存在し、Storage Nodeにアクセスする。
Introducerの役割とは。

Client/Gatewayは、URLもしくはRESTのインターフェースを提供
object storeとする。

Nodeは、geographically distant を考慮できる？


Compare and Contrast, versus SAN
Tahoeはdownloadを同時並行的に多数のノードから行える。

hash-tree
===============================================================================

p2pのデータブロックの破損や改竄の検証処理に使用している。

たとえば、ZFS, Apache Wave, Git, Tahoe-LAFS, Bitcoin
Cassandra, Riak

Treeの部分的な枝のみで、下位構造の検証が行えるため、
壊れている部分は再度ダウンロードするような、ボトムアップ的な検証ができる。

deduplicate
===============================================================================
結論からいうと、やってない。

Q15: If upload the same file again and again, Tahoe-LAFS will return the same capability.
How does Tahoe-LAFS identify that the client is same,
when I upload files mutiple times, is it based on node ID?

A: For immutable files this is true—the resulting capability will be the same each time
you upload the same file contents.
The capability is derived from two pieces of information:
The content of the file and the "convergence secret".
By default, the convergence secret is randomly generated by the node when it first starts up,
then stored in the node's base directory (~/.tahoe) and re-used after that.
So the same file content uploaded from the same node will always have the same cap string.
Uploading the file from a different node with a different convergence secret would result
in a different cap string—and in a second copy of the file's contents stored on the grid.
If you want files you upload to converge (also known as "deduplicate")
with files uploaded by someone else,
just make sure you're using the same convergence secret as they are.

Q15.1: Isn't deduplication dangerous? Can someone figure out whether or not I have a certain file?

A: It is dangerous, even more so than most people realize!
But, Tahoe-LAFS provides a defense: git/docs/convergence-secret.rst.

convergenc-secretとは


TODO and FAQ
*******************************************************************************

difference between Tahoe-LAFS and Freenet
https://tahoe-lafs.org/pipermail/tahoe-dev/2011-July/006560.html

revocation of read-access to an immutable file
https://tahoe-lafs.org/pipermail/tahoe-dev/2011-June/006424.html


Provider-independent security

provides reliable

fault-tolerant storage

暗号化には何を使っているのか

spacemonkeyとの差分は。


ACLはどこまでやっているのか、tamiasは？





