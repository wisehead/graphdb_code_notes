#1.set_node_info

```
set_node_info
--let mut msg = DataSetMsg::default();
--msg.header.push(MetaClient::get().get_node_address());
--Ok(msg)
```