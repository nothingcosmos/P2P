src
###############################################################################

main
*******************************************************************************

main.go
===============================================================================
os.Exit()にMainを登録して実行。
引数処理して

cli.CLI{...}
cli.Run()

Run(args)メソッド自体は誰かが実装している。

commands.go
===============================================================================

上記のcliで起動するCommands map[String]を登録する。
CommandFactory

command
*******************************************************************************

event.go
===============================================================================
force_leave.go
===============================================================================
join.go
===============================================================================

client, err := RPCClient(* rpcAddr)

defer client.Close()

n, err := client.Join(addrs, replayEvents)

//deferはこの関数が抜けた際のcallbackを登録する。

keygen.go
===============================================================================
leave.go
===============================================================================
members.go
===============================================================================
monitor.go
===============================================================================
rpc.go
===============================================================================
デフォルト
127.0.0.1:7373

flagは引数で指定する。

version.go
===============================================================================


command/agent
*******************************************************************************

agent.go
===============================================================================

func (a * Agent) Join(addrs []string, replay bool)
a.serf.Join()


command.go
===============================================================================
config.go
===============================================================================
event_handler.go
===============================================================================
event_handler_mock.go
===============================================================================
flag_slice_value.go
===============================================================================
gated_writer.go
===============================================================================
invoke.go
===============================================================================
ipc.go
===============================================================================
ipc_event_stream.go
===============================================================================
ipc_log_stream.go
===============================================================================
log_levels.go
===============================================================================
log_writer.go
===============================================================================
rpc_client.go
===============================================================================

serf
*******************************************************************************

broadcast.go
===============================================================================
coalesce.go
===============================================================================
coalesce_member.go
===============================================================================
coalesce_user.go
===============================================================================
config.go
===============================================================================
delegate.go
===============================================================================
event.go
===============================================================================
event_delegate.go
===============================================================================
lamport.go
===============================================================================

messages.go
===============================================================================





serf.go
===============================================================================

Serfはsingle nodeを表現する

// Join joins an existing Serf cluster. Returns the number of nodes
// successfully contacted. The returned error will be non-nil only in the
// case that no nodes could be contacted. If ignoreOld is true, then any
// user messages sent prior to the join will be ignored.
func (s * Serf) Join(existing []string, ignoreOld bool) (int, error) {

  s.joinLock.Lock()
  defer s.joinLock.Unlock()

  s.memberlist.Join(existing)
  if num > 0 {
    s.broadcastJoin(s.clock.Time()) //clock
  }
  return num, err

//memberlistにjoinして、broadcastJoinするだけ？


func (s * Serf) broadcastJoin(ltime LamportTime) error {

  msg := messageJoin(LTime:Node)
  s.clock.Witness(ltime)
  s.handleNodeJoinIntent(&msg)

  s.broadcast(mesageJoinType, &msg, nil)

//LamportTime


snapshot.go
===============================================================================

memberlist
*******************************************************************************

broadcast.go
===============================================================================
config.go
===============================================================================
delegate.go
===============================================================================
event_delegate.go
===============================================================================
memberlist.go
===============================================================================

// Join is used to take an existing Memberlist and attempt to join a cluster
// by contacting all the given hosts and performing a state sync. Initially,
// the Memberlist only contains our own state, so doing this will cause
// remote nodes to become aware of the existence of this node, effectively
// joining the cluster.
//
// This returns the number of hosts successfully contacted and an error if
// none could be reached. If an error is returned, the node did not successfully
// join the cluster.
func (m * Memberlist) Join(existing []string) (int, error) {

  existingすべてに m.resolveAddr(exist)
  m.pushPullNode(adr, port, true) これがfull state sync




net.go
===============================================================================
//ここに全部net系がそろってるっぽい。




queue.go
===============================================================================
security.go
===============================================================================
state.go
===============================================================================

// pushPullNode does a complete state exchange with a specific node.
func (m * Memberlist) pushPullNode(addr []byte, port uint16, join bool) error {

  m.sendAndReceiveState(addr, port, join)
  m.verifyProtocol()
  m.mergeState(remote)
  //delegate
  m.config.Delegate.MergeRemoteState()



util.go
===============================================================================

template ::
  ###############################################################################
  *******************************************************************************
  ===============================================================================

