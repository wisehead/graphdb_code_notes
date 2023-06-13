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
----let receive_result = timeout(heartbeat, self.rcv.next()).await;
----match receive_result {
------Ok(Some(Message::Raft(m))) => {
--------let msg_type = m.get_msg_type();
--------if !snapshot_received && msg_type == MessageType::MsgHeartbeat {
                        arcgraph_log::raft_debug!(
                            "[raft] MsgHeartbeat message received, snapshot_received: {}, has_leader: {}, {:?}",
                            snapshot_received,
                            self.has_leader(),
                            m
                        );
--------} else {
----------if let Err(e) = self.step(*m) {
                            arcgraph_log::raft_warn!(
                                "step error, {:?}, msg_type: {:?}, snapshot_received: {}",
                                e,
                                msg_type,
                                snapshot_received
                            );
                        }
----------if msg_type == MessageType::MsgSnapshot {
                            snapshot_received = true;
--------}
------}

------Ok(Some(Message::Propose { proposal, chan })) => {
--------if !self.is_leader() {
----------self.send_wrong_leader(chan);
--------} else {
----------let log: Vec<data_type::LogEntry> = deserialize(&proposal).unwrap();
----------merger.add(proposal, chan);
----------self.take_and_propose(&mut merger);

------Ok(Some(Message::RequestId { chan })) => {
--------if !self.is_leader() {
----------self.send_wrong_leader(chan);
--------} else {
----------self.send_leader_id(chan);
------------chan.send(RaftResponse::RequestId {leader_id: self.leader(),}
--------}
------}
----let on_ready_now = Instant::now();
----self.on_ready().await 
    // Do checkpoint
----self.do_checkpoint(false).await;
--loop
```