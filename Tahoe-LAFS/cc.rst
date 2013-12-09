Tahoe-LAFS
###############################################################################

top levelのクラス
*******************************************************************************

zope/interfaceとtwistedのserviceを使用している。

interfaces.pyで定義、コメントが記述されており、ここをtopに追っていけば分かる。

interfaces.pyをimportしているファイルの一覧を示す。 ::

  blacklist.py:from allmydata.interfaces import IFileNode, IFilesystemNode
  check_results.py:from allmydata.interfaces import ICheckResults, ICheckAndRepairResults, \
  client.py:from allmydata.interfaces import IStatsProducer, SDMF_VERSION, MDMF_VERSION
  codec.py:from allmydata.interfaces import ICodecEncoder, ICodecDecoder
  control.py:from allmydata.interfaces import RIControlClient, IFileNode
  dirnode.py:from allmydata.interfaces import IFilesystemNode, IDirectoryNode, IFileNode, \
  key_generator.py:from allmydata.interfaces import RIKeyGenerator
  nodemaker.py:from allmydata.interfaces import INodeMaker
  stats.py:from allmydata.interfaces import RIStatsProvider, RIStatsGatherer, IStatsProducer
  storage_client.py:from allmydata.interfaces import IStorageBroker, IDisplayableServer, IServer
  unknown.py:from allmydata.interfaces import IFilesystemNode, MustNotBeUnknownRWError, \
  uri.py:from allmydata.interfaces import IURI, IDirnodeURI, IFileURI, IImmutableFileURI, \


各ディレクトリの下 ::

  frontends/drop_upload.py:from allmydata.interfaces import IDirectoryNode
  frontends/ftpd.py:from allmydata.interfaces import IDirectoryNode, ExistingChildError, \
  frontends/sftpd.py:from allmydata.interfaces import IFileNode, IDirectoryNode, ExistingChildError, \

  immutable/checker.py:from allmydata.interfaces import IValidatedThingProxy, IVerifierURI
  immutable/encode.py:from allmydata.interfaces import IEncoder, IStorageBucketWriter, \
  immutable/filenode.py:from allmydata.interfaces import IImmutableFileNode, IUploadResults
  immutable/layout.py:from allmydata.interfaces import IStorageBucketWriter, IStorageBucketReader, \
  immutable/literal.py:from allmydata.interfaces import IImmutableFileNode, ICheckable
  immutable/repairer.py:from allmydata.interfaces import IEncryptedUploadable
  immutable/upload.py:from allmydata.interfaces import IUploadable, IUploader, IUploadResults, \

  introducer/client.py:from allmydata.interfaces import InsufficientVersionError
  introducer/old.py:from allmydata.interfaces import InsufficientVersionError

  mutable/filenode.py:from allmydata.interfaces import IMutableFileNode, ICheckable, ICheckResults, \
  mutable/layout.py:from allmydata.interfaces import HASH_SIZE, SALT_SIZE, SDMF_VERSION, \
  mutable/publish.py:from allmydata.interfaces import IPublishStatus, SDMF_VERSION, MDMF_VERSION, \
  mutable/repairer.py:from allmydata.interfaces import IRepairResults, ICheckResults
  mutable/retrieve.py:from allmydata.interfaces import IRetrieveStatus, NotEnoughSharesError, \
  mutable/servermap.py:from allmydata.interfaces import IServermapUpdaterStatus

  storage/immutable.py:from allmydata.interfaces import RIBucketWriter, RIBucketReader
  storage/mutable.py:from allmydata.interfaces import BadWriteEnablerError
  storage/server.py:from allmydata.interfaces import RIStorageServer, IStatsProducer

  web/check_results.py:from allmydata.interfaces import ICheckAndRepairResults, ICheckResults
  web/common.py:from allmydata.interfaces import ExistingChildError, NoSuchChildError, \
  web/directory.py:from allmydata.interfaces import IDirectoryNode, IFileNode, IFilesystemNode, \
  web/filenode.py:from allmydata.interfaces import ExistingChildError, SDMF_VERSION, MDMF_VERSION
  web/info.py:from allmydata.interfaces import IDirectoryNode, IFileNode, MDMF_VERSION
  web/root.py:from allmydata.interfaces import IFileNode
  web/status.py:from allmydata.interfaces import IUploadStatus, IDownloadStatus, \


I Immutable
M Mutable
R readable
W writable




mutable/immutable
*******************************************************************************

mutableとimmutableがいるのが特徴


mutableは、publish, repairer, retrieve

immutableは、encode, upload, repairer



おいかた

initから

getから

putから

ACL相当から


immutable dir
mutable
が存在するな。

read/writeのコントロールの違いだっけか。


client.py
*******************************************************************************
implementsはzopeのモジュールらしい。

主に、interfaces.pyに役割やコメントが記述されている。
IClient(Interface)ってのが定義されており、こちらのコメントが参考になる。



upload
*******************************************************************************

twistedのserviceに"upload"を登録している。

service



HashTree
*******************************************************************************

HashTree ::

  immutable/checker.py:from allmydata.hashtree import IncompleteHashTree
  immutable/checker.py:        self.block_hash_tree = hashtree.IncompleteHashTree(self.num_blocks)
  immutable/checker.py:            share_hash_tree = IncompleteHashTree(vcap.total_shares)
  immutable/checker.py:            cht = IncompleteHashTree(vup.num_segments)
  immutable/encode.py:from allmydata.hashtree import HashTree
  immutable/encode.py:        t = HashTree(self._crypttext_hashes)
  immutable/encode.py:        t = HashTree(block_hashes)
  immutable/encode.py:        t = HashTree(self.share_root_hashes)
  immutable/encode.py:            # the HashTree is given a list of leaves: 0,1,2,3..n .
  immutable/upload.py:        # Encoder.send_all_share_hash_trees. We use an IncompleteHashTree
  immutable/upload.py:        # (instead of a HashTree) because we don't require actual hashing
  immutable/upload.py:        ht = hashtree.IncompleteHashTree(total_shares)
  mutable/publish.py:            h = hashtree.IncompleteHashTree(old_segcount)
  mutable/publish.py:            t = hashtree.HashTree(blockhashes)
  mutable/publish.py:        share_hash_tree = hashtree.HashTree(self.sharehash_leaves)
  mutable/retrieve.py:        self.share_hash_tree = hashtree.IncompleteHashTree(N)
  mutable/retrieve.py:                self._block_hash_trees[i] = hashtree.IncompleteHashTree(self._num_segments)


===============================================================================
===============================================================================

template ::
  ###############################################################################
  *******************************************************************************
  ===============================================================================

