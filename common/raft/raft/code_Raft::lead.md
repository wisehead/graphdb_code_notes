#1.Raft::lead

```
Raft::lead
--let node = RaftNode::new_leader(
            self.graph_id,
            self.partition_id,
            self.host_id,
            self.rx,
            self.tx.clone(),
            node_id,
            self.store,
            &self.logger,
            self.cfg.clone(),
            self.storage,
            cluster,
            self.do_recovery,
        );
--let node_handle = tokio::spawn(async {node.run()})
--let e = tokio::try_join!(node_handle);
```