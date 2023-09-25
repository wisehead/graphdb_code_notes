#1.sync_system_graph

```
sync_system_graph
--if MetaManager::get()
        .get_graph_meta_data(cluster_id, systemdb_constants::SYSTEM_GRAPH_ID)
        .is_err()
----create_system_graph(cluster_id).await;
```