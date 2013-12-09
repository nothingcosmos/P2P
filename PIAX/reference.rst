Reference
###############################################################################

http://live-e.naist.jp/sensor_overlay2008/2/doc/teranishi-sensor-overlay-2nd.pdf
*******************************************************************************

AgentのAPIやAgentのdiscoveryの説明

2008年の資料で、PIAX3.0と比較すると若干Agentの実装が古い。

http://www.slideshare.net/kibayos/kibayospiax-skipgraph071207
*******************************************************************************

PIAXのDiscoveryとAgentに関して

SkipGraph

http://live-e.naist.jp/sensor_overlay2008/doc/yoshida-sensor-overlay-080705.pdf
*******************************************************************************
SkipGraphや検索について

unbreakableの研究成果の紹介

Chordの改良らしい。


DDLL SkipGraph
*******************************************************************************
http://live-e.naist.jp/sensor_overlay/5/doc/abe.pdf

SkipGraphの耐障害性が弱い。

分散排他制御が弱い

ノードが突然離脱した場合に困る

DDLL 分散双方向連結リストで問題解決

SkipGraph Atomic Ring Maintenance Protocol


DDLLは、分散排他制御不要。

スタビライズ不要。

uniqなキーが必要。かつ隣しか知らない。障害や離脱が発生した際に困る。どう修復するか。

左右に複数個持つと。

PIAX3.0に実装。同時数百のjoinでも問題ないSkipGraphが完成


一貫性保証に関して
*******************************************************************************
http://www.slideshare.net/kibayos/kibayosov090922

::
  *******************************************************************************
  ===============================================================================

