#1.recovery

```
recovery
--if refresh_cache && memory_engine::MemoryEngine::is_global_topology_cache_enabled() 
----let instances = GraphInstances::get();
----instances
            .recovery_partition_data(graph_id, partition_id)
            .await
            .unwrap();
```