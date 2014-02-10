SEDA
###############################################################################





thread runをひたすら探してみる
*******************************************************************************

elise@elise-desktop:~/p2p/cassandra/src/java/org/apache/cassandra$ grep run\( */*
auth/Auth.java:                                              public void run()
auth/PasswordAuthenticator.java:                                              public void run()
cache/AutoSavingCache.java:                public void run()
concurrent/DebuggableScheduledThreadPoolExecutor.java:        public void run()
concurrent/DebuggableScheduledThreadPoolExecutor.java:                runnable.run();
db/BatchlogManager.java:                public void run()
db/ColumnFamilyStore.java:            public void run()
db/ColumnFamilyStore.java:                public void run()
db/ColumnFamilyStore.java:            public void run()
db/CounterMutationVerbHandler.java:                public void run()
db/HintedHandOffManager.java:            public void run()
db/HintedHandOffManager.java:            public void run()
db/HintedHandOffManager.java:                    public void run()
db/HintedHandOffManager.java:            public void run()
db/Memtable.java:        public void run()
db/MeteredFlusher.java:    public void run()
gms/Gossiper.java:        public void run()
hadoop/AbstractColumnFamilyRecordWriter.java:        public abstract void run();
hadoop/ColumnFamilyRecordWriter.java:        public void run()
locator/DynamicEndpointSnitch.java:            public void run()
locator/DynamicEndpointSnitch.java:            public void run()
net/IncomingStreamingConnection.java:    public void run()
net/IncomingTcpConnection.java:    public void run()
net/MessageDeliveryTask.java:    public void run()
net/MessagingService.java:            public void run()
net/MessagingService.java:        public void run()
net/OutboundTcpConnection.java:    public void run()
net/OutboundTcpConnection.java:            public void run()
repair/Differencer.java:    public void run()
repair/Differencer.java:        task.run();
repair/RepairMessageVerbHandler.java:                task.run();
repair/StreamingRepairTask.java:    public void run()
repair/Validator.java:    public void run()
scheduler/RoundRobinScheduler.java:            public void run()
service/AbstractWriteResponseHandler.java:            callback.run();
service/CassandraDaemon.java:        public void run()
service/CassandraDaemon.java:            public void run()
service/GCInspector.java:            public void run()
service/LoadBroadcaster.java:            public void run()
service/MigrationManager.java:                public void run()
service/ReadCallback.java:        public void run()
service/ScheduledRangeTransferExecutorService.java:    public void run()
service/StorageProxy.java:                runnable.run();
service/StorageProxy.java:        public final void run()
service/StorageProxy.java:        public final void run()
service/StorageProxy.java:        public void run()
service/StorageService.java:                    public void run()
service/StorageService.java:        createRepairTask(nextRepairCommand.incrementAndGet(), keyspaceName, ranges, isSequential, isLocal, columnFamilies).run();
service/StorageService.java:            public void run()
service/StorageService.java:        onFinish.run();
streaming/ConnectionHandler.java:        public void run()
streaming/ConnectionHandler.java:        public void run()
streaming/StreamManager.java:            public void run()
streaming/StreamManager.java:            public void run()
streaming/StreamSession.java:            public void run()
thrift/CustomTThreadPoolServer.java:        public void run()
thrift/ThriftServer.java:        public void run()
tracing/Tracing.java:                public void run()
tracing/Tracing.java:            public void run()
transport/Client.java:    public void run() throws IOException
transport/Client.java:        new Client(host, port, encryptionOptions).run();
transport/Server.java:                run();
transport/Server.java:    private void run()
utils/BackgroundActivityMonitor.java:        public void run()
utils/ExpiringMap.java:            public void run()
utils/FastByteComparisons.java:              public Object run() {
utils/ResourceWatcher.java:        public void run()
utils/ResourceWatcher.java:                    callback.run();
utils/WrappedRunnable.java:    public final void run()


elise@elise-desktop:~/p2p/cassandra/src/java/org/apache/cassandra$ grep run\( */*/*
db/commitlog/BatchCommitLogExecutorService.java:            firstTask.run();
db/commitlog/CommitLog.java:        public void run()
db/commitlog/CommitLog.java:            run();
db/commitlog/CommitLogAllocator.java:                        r.run();
db/commitlog/CommitLogAllocator.java:            public void run()
db/commitlog/CommitLogAllocator.java:            public void run()
db/commitlog/CommitLogAllocator.java:            public void run()
db/commitlog/CommitLogAllocator.java:                        public void run()
db/commitlog/PeriodicCommitLogExecutorService.java:                    r.run();
db/commitlog/PeriodicCommitLogExecutorService.java:            public void run()
db/compaction/CompactionManager.java:        public void run()
db/compaction/CompactionManager.java:                    public void run()
db/compaction/CompactionManager.java:            public void run()
db/compaction/CompactionManager.java:            public void run()
db/compaction/CompactionTask.java:        run();
db/index/SecondaryIndex.java:            public void run()
hadoop/cql3/CqlRecordWriter.java:        public void run()
io/sstable/SSTableDeletingTask.java:    public void run()
io/sstable/SSTableDeletingTask.java:            public void run()
io/sstable/SSTableReader.java:                public void run()
io/sstable/SSTableReader.java:            public void run()
io/sstable/SSTableSimpleUnsortedWriter.java:        public void run()
io/util/FileUtils.java:            public void run()


上記のThreadの作り
===============================================================================

===============================================================================



*******************************************************************************

呼び出しの管理
===============================================================================
Runnable runnable = new Runnable()

  scheduleAllDeliveries()

StorageService.optionalTasks.scheduleWithFixedDelay(runnable, 10, 10, TimeUnit.MINUTES);

StorageService.tasks.schedule()


service/StorageService.java
===============================================================================

concurrent/DebuggableScheduledThreadPoolExecutor.java

public class DebuggableScheduledThreadPoolExecutor extends ScheduledThreadPoolExecutor

protected Future<?> compact()



===============================================================================
===============================================================================

###############################################################################

*******************************************************************************

*******************************************************************************

===============================================================================
===============================================================================
