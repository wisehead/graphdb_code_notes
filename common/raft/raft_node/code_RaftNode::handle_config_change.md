#1.RaftNode::handle_config_change

```
RaftNode::handle_config_change
--let seq: u64 = deserialize(entry.get_context())?;
--let change: ConfChange = protobuf::Message::parse_from_bytes(entry.get_data())?;
--let id = change.get_node_id();
--let change_type = change.get_change_type();
```