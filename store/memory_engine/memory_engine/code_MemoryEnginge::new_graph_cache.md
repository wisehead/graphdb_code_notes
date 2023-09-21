#1.MemoryEnginge::new_graph_cache

```
MemoryEngine::new_graph_cache
--let graph_name = MetaHelper::get().get_graph_name_by_id(graph_id).unwrap();
--if Config::get(None)
            .memory_engine
            .is_graph_topology_cache_enabled(&graph_name)
        {
----GRAPH_CACHE
                .graph_caches
                .entry(graph_id)
                .or_insert_with(|| Arc::new(GraphCache::new(graph_id)));

----GRAPH_CACHE
                .index_buffers
                .entry(graph_id)
                .or_insert_with(|| Arc::new(IndexBuffer::new()));
            true
        }
```