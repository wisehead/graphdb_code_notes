#1.GraphInstances::add_new_graph_instance

```
GraphInstances::add_new_graph_instance
--let graph_instance = self.init_graph_instance(graph_id, meta_cache).await;
--let mut map = self.graph_map.write().unwrap();
--map.insert(graph_id, Arc::new(graph_instance));
```