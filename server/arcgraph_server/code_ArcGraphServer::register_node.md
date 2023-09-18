#1.ArcGraphServer::register_node

```
ArcGraphServer::register_node
--let cluster_info_msg = if standalone_mode {
----let node = Node::default();
------get_server_node_info
----let cluster_id = node.cluster_id.unwrap();
----MetaManager::get().register_node(cluster_id, node).await?
--} else {
----RegisterNodeRequest::dispatch(()).await?
--meta_api::MetaHelper::initialize(cluster_info_msg)?;
--if !standalone_mode {
----tokio::spawn(Self::sync_heartbeat());
```