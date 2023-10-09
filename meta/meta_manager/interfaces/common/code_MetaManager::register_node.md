#1.MetaManager::register_node

```
MetaManager::register_node
--let cluster_info = if let Some(cluster) = self.clusters.get(&cluster_id) {
            cluster.clone()
--} else {
            // The first node of current cluster
            let cluster = Arc::new(ClusterInfo::init(cluster_id).await?);
            self.clusters.insert(cluster_id, cluster.clone());
            new_cluster = true;

            cluster
--};
--let node_id = node.id;
--let node = Arc::new(node);
--cluster_info.nodes.insert(node_id, node.clone());
--let mut kvs = HashMap::new();
--let schema_key = format_meta_key!(cluster_id, "{}{}", K_NODE_KEY_PREFIX, node_id);
--let node_str = serde_json::to_string(&node)?;
--if new_cluster {
----if initdb::init_internal_resource(cluster_id).await.is_err() {
                meta_error!("fail to init SYSTEM graph for cluster {}", cluster_id);
            }
            // persist cluster information
----let cluster_ids: Vec<ClusterId> = self.clusters.iter().map(|g| *g.key()).collect();
----kvs.insert(
                meta_common::constants::K_CLUSTERS.to_string(),
                serde_json::to_string(&cluster_ids)?,
            );
--}
--self.meta_store.txn_put(&kvs).await?;
--let check_node =
            |x: &Node| -> bool { x.id != node_id && x.node_status.eq(&Some(NodeStatus::Online)) };
--let node_vec: Vec<_> = cluster_info
            .nodes
            .iter()
            .filter(|iter| check_node(iter.value()))
            .map(|iter| iter.value().clone())
            .collect();
--if !node_vec.is_empty() {
----let node_msg = NodeMsg {
                delete: false,
                node: util::serialize_object(&node)?,
            };

----for iter in node_vec {
                let update_func =
                    ComputeGrpcClient::update_node(iter.address.clone(), node_msg.clone());
                // TODO: what if fail to update node? retry, need have a notification service, all
                // operation need retry util
                BackgroundExecutor::instance().spawn(async move {
                    let result = update_func.await;
                    if result.is_err() {
                        meta_error!("{:?}", result);
                    }
                });
            }
--}
```

#2.caller

```
- 单机版
	- ArcGraphServer::register_node 
- 分布式版
	- handle_register_node
```