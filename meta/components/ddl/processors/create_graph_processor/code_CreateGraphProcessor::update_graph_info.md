#1.CreateGraphProcessor::update_graph_info

```
CreateGraphProcessor::update_graph_info
--let mut rnd = rand::thread_rng();
--let mut start_id = rnd.gen::<i32>() as usize;
--let node_count = all_nodes.len();

--self.inner.op.graph_id = Some(graph_id);

--let replica_number = if is_standalone_mode() {
            self.inner.op.replica_number = Some(1);
            1
--} else if self.inner.op.replica_number.is_none() {
            let number: u32 = config::MetaConfigManager::instance()
                .get_value_into::<u32>(config::meta_config_item::META_PARTITION_REPLICA_NUMBER);
            self.inner.op.replica_number = Some(number);
            number
--} else {
            self.inner.op.replica_number.unwrap()
        };

--for p_id in 0..self.inner.op.partition_number {
            let j = start_id % node_count;
            let mut peer_info: Vec<RaftPeerInfo> = vec![];

            for i in 0..replica_number as usize {
                let index = (j + i) % node_count;
                peer_info.push(RaftPeerInfo {
                    node_id: all_nodes[index].id,
                    peer_id: IdGenerator::instance().get_id() as RaftPeerId,
                    peer_role: Some(PeerRole::Voter),
                });
            }

            // TODO remote init raft leader
            self.inner
                .partition_leaders
                .insert(p_id, peer_info[0].clone());

            // TODO remote init raft follower
            self.inner.partition_peer_info.push(PartitionPeerInfo {
                id: p_id,
                peer_info,
            });
            start_id += 1;
--}
```