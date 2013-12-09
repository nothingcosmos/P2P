src
###############################################################################

本格的に読む時間ないので、srcをざらっと眺めた感想

cpp/hで作成

https://github.com/bitcoin/bitcoin

Bitcoin

The U.S.
Department of Defense is conducting research
on P2P networks as part of its modern network warfare strategy.[38] In May, 2003,
Anthony Tether, then director of DARPA,
testified that the U.S. military uses P2P networks.

Wireless community network, Netsukuku

Dalesa a peer-to-peer web cache for LANs (based on IP multicasting).

Open Garden,
connection sharing application that shares Internet access
with other devices using Wi-Fi or Bluetooth.

Research like the Chord project,
the PAST storage utility, the P-Grid, and the CoopNet content distribution system.


構成要素
*******************************************************************************

boost

bloomfilter

crypter

leveldb

json

rpc jsonベースで独自実装。json_spirit仕様

qtってのがでかい。 QTのUIを使うらしい。 serverとか。 walletまわりのutilとか。

uint256

bitcoinの用語
===============================================================================

mining

wallet

Proof of work
===============================================================================


shaをひたすら計算して、未発掘のhashかどうか、他のNodeに未発掘か認証してもらい、
未発掘のものだったら、自分のものにしていい。

hashなので、空間に制限があって、
他のNodeに未発掘かどうか聞いて回って認証してもらう必要があるため、
リソースが必要。またshaの計算を高速化する必要がある。



networkをsplitして、cloneを作りまくって別networkを作成し、
認証しあえば乗っ取りできるのでは？


template ::
  ###############################################################################
  *******************************************************************************
  ===============================================================================

