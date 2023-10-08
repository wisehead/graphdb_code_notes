#1.GraphMetaData::fetch_nodes

```
GraphMetaData::fetch_nodes
--let response = meta_store
            .txn_get(&format_meta_key!(cluster_id, K_NODE_KEY_PREFIX), true)
            .await?;
--for kv in response {
----let value_str = kv.value_str();
----if value_str.is_err() {
                continue;
            }
----let node = Node::from(value_str?);
----nodes.insert(
                node.id,
                Arc::new(Node {
                    node_status: Some(NodeStatus::Offline),
                    ..node
                }),
            );
--}            
```