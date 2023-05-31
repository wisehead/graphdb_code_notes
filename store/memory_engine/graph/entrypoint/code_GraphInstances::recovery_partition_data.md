#1.GraphInstances::recovery_partition_data

```
GraphInstances::recovery_partition_data
--let graph_name = MetaClient::get().get_graph_name_by_id(graph_id)?;
--let (filter_vertices, filter_edges) = if let Some(config) = 
			Config::get(None).memory_engine.enable_topology_cache_per_graph_labels(&graph_name) {
(config.vertex_labels.clone().map_or_else(Vec::default, |v| v), config.edge_labels.clone().map_or_else(Vec::default, |v| v))
--let strategy = TopoLoadStrategy {
                filter_vertices,
                filter_edges,
                skip_edge_list: !Config::get(None).memory_engine.dev_make_edge_list(),
                skip_vertex_list: !Config::get(None).memory_engine.dev_make_vertex_list(),
            };
--g.initialize_topology_cache_with_partitions(&[partition_id], strategy).await?;
```