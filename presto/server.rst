PrestoServer
###############################################################################

依存ライブラリ
*******************************************************************************
https://github.com/airlift/airlift

概要をざっくり把握するのはこれ
http://d.hatena.ne.jp/tagomoris/20131224/1387879021


PrestoServer
===============================================================================
thread run

modulesのload
ServerMainModule()

BootStrap modules

injector
PluginManager
CatalogManager
Announcer

installCodeacheGcTrigger()で終わり
  usedを参照して、しきい値以下ならSystem.gc()
  setDaemon()して放置


ServerMainModule
===============================================================================

//coordinatorの場合
install new CoordinatorModule()
discoveryBinder
bindFailureDetector


あとはbinderにbind bind
TaskResource
TaskManager
LocalExecutionPlanner
ExpressionCompiler

ExecuteResource

ローカルストレージはデフォルトH2

PluginManager
===============================================================================

AtrifactResolver
connectorManager
systemTablesManager

pomを参照してclass loading



CatalogManager
===============================================================================

Announcer
===============================================================================

TaskResource
===============================================================================
final TaskManager
これはただのコンテナ

createOrUpdateTask(taskId, TaskUpdateRequest getFragment getSources getOutputIds
entity(taskInfo).build()

getTaskInfo
cancelTask
getResults
abortResults

全部annotationベースで修飾されてる。json put/get

TaskUpdateRequest
===============================================================================
Session session
PlanFragment fragment
List<TaskSource> sources
OutputBuffers outputIds

HttpRemoteTask
===============================================================================
ここにきた段階で、session planFragment sources outputBuffersは細切れである。

StateMachine

OutputReceiver

synchronized scheduleUpdate()
でTaskUpdateRequestを作成し、serverにpost (httpでpost)

httpClientでexecuteAsync, 戻りはListenableFuture<JsonResponse<TaskInfo>>

taskの操作は全部上記と同様。

taskInfoFetcherとかもいる。


execution
===============================================================================
ThreadContextClassLoader
Plugins

createExchangeExecutor()
return Executors.newCachedThreadPool(Threads.daemonThreadsNamed("exchange-callback-%s"));





OutputReceiver
===============================================================================

===============================================================================
===============================================================================


TODO
*******************************************************************************

source

task build

OutputReceiver
final TaskManager
  ただのコンテナ

*******************************************************************************
*******************************************************************************

===============================================================================
===============================================================================

template ::
  ###############################################################################
  *******************************************************************************
  ===============================================================================

