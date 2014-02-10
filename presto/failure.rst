FailureDetector
###############################################################################

clientからcoordinatorを監視するはず

Binder binder
===============================================================================

inject.Binder

binder.bind(HeatbeatFailureDetector)
binder.bind(FailureDetector)


FailureDetector interface
===============================================================================
for failure detector

start()
  updateMonitoredServices()

DIでbindしたobjの引数を指定できるのか。


いいなこの書き方
Iterabletransformer.on(tasks.values()).select(isFailedPredicate()).transform(serviceGetter())).set())

presto/utilで定義している。
guavaにのみ依存している。のかな。


updateMonitoredServices()
===============================================================================

MonitoringTask

enable
  ping()
    success
    recordFailure
  updateState()
    update timestamp nanoTime()

disable
  disableTimeStamp

failedの判定は、
successTransitionTimestamp == null ||
Duration.nanosSince(successTransitionTimestamp).compareTo(warmupInterval) < 0;

executeAsync()して、
5sec以内にpingを待つのか


Config
===============================================================================

failureRatioThreshold = 0.01 //1%

heatbeatInterval 500ms
warmupInterval 5sec
expirationGraceInterval 10minutes

annotation
===============================================================================

@DecimalMin
@DecimalMax


