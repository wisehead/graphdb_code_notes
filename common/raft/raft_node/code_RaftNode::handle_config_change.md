#1.RaftNode::handle_config_change

```
RaftNode::handle_config_change
--let seq: u64 = deserialize(entry.get_context())?;
--let change: ConfChange = protobuf::Message::parse_from_bytes(entry.get_data())?;
--let id = change.get_node_id();
--let change_type = change.get_change_type();
--let _meta = MetaClient::get();
--match change_type {
----ConfChangeType::AddNode | ConfChangeType::AddLearnerNode => {
------let (addr, host_id): (String, u64) = deserialize(change.get_context())?;
------let peer_role = if change_type == ConfChangeType::AddNode {
                    PeerRole::Voter
                } else {
                    PeerRole::Learner
                };
------self.add_peer(&addr, id, host_id, peer_role);

----ConfChangeType::RemoveNode => {
------if change.get_node_id() == self.id() {
--------self.should_quit = true;
------else
--------self.peers.remove(&change.get_node_id()); 

--if let Ok(cs) = self.apply_conf_change(&change) {
----let last_applied = self.raft.raft_log.applied;     
----let snapshot = prost::bytes::Bytes::from(self.store.snapshot().await.unwrap());
------let store = self.mut_store();
------store.set_conf_state(&cs).unwrap();
------store.create_snapshot(snapshot).unwrap();          
```