#1.RaftNode::do_checkpoint

```
RaftNode::do_checkpoint
--if self.is_leader() {
----if now > self.last_snap_time + self.cfg.snapshot_interval {
------let _ = checkpoint(graph_id, partition_id, idx, &logs).await;
------store.compact(idx).unwrap();
```

#2.caller

```
async_main
--init_raft/handle_graph_action
----init_graph_partition_raft
------Raft::lead
--------RaftNode::run

```