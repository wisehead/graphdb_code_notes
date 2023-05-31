#1.RaftNode::run

```
RaftNode::run
--let mut merger = Merger::new(
            self.cfg.proposal_batch_size,
            self.cfg.proposal_batch_timeout,
        );
--self.do_report_status();
--process_recovery
----recovery(graph_id, partition_id, logs, true)
--self.update_pre_leader_id(self.leader());
--loop
----self.update_pre_leader_id(self.leader());
----match timeout(heartbeat, self.rcv.next()).await {
------Timeout::poll
--------had_budget_before = coop::has_budget_remaining();
----self.do_checkpoint().await;
--
```