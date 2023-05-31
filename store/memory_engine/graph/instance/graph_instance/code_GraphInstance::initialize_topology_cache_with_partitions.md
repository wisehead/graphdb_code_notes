#1.GraphInstance::initialize_topology_cache_with_partitions
```
GraphInstance::initialize_topology_cache_with_partitions
--MemoryEngine::new_graph_topology_cache(self.id);
--MemoryEngine::new_graph_property_cache(self.id);
--let graph_topo_cache = MemoryEngine::get_graph_topo_entry_by_id(&self.id)?;
--graph_topo_cache.set_graph_load_finished(false);
--self.load_all_edges(partitions, strategy.skip_edge_list, strategy.skip_vertex_list, strategy.filter_edges.as_slice())
            .await?;
--self.load_all_vertexes(partitions, strategy.skip_vertex_list, strategy.filter_vertices.as_slice())
            .await?;
--graph_topo_cache.set_graph_load_finished(true);
```