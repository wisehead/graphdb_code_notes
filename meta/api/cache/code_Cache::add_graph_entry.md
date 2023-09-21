#1.Cache::add_graph_entry

```
Cache::add_graph_entry
--let graph_id = graph.id;
--self.graph_names.insert(graph.name.clone(), graph_id);
--self.graph_data.insert(
            graph.id,
            Arc::new(GraphMetaData {
                graph: RwLock::new(graph),
                partition_id_leader_map: RwLock::new(partition_leaders),
                partition_peer_info: RwLock::new(partition_peer_info),
                edge_schemas: Arc::new(Default::default()),
                vertex_schemas: Arc::new(Default::default()),
                index: Arc::new(Default::default()),
                edge_type_name_map: Arc::new(Default::default()),
                vertex_type_name_map: Arc::new(Default::default()),
                index_name_map: Arc::new(Default::default()),
            }),
        );
```