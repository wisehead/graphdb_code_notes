#1.CreateGraphProcessor::prepare

```
CreateGraphProcessor::prepare
--let graph = self.build_graph()?;
--if work_as_arc_server {
----let helper = MetaHelper::get();
            helper.add_graph_entry(
                graph,
                self.inner.partition_leaders.clone(),
                self.inner.partition_peer_info.clone(),
            )?;
            if let Ok(meta_cache) = helper.get_graph_meta_cache(graph_id) {
                store_api::create_graph(graph_id, meta_cache).await;
            }
            partition_raft::init_graph_partition_raft(graph_id).await;
--} else {
            let cluster = MetaManager::get().get_cluster(cluster_id)?;
            cluster.add_graph_entry(
                graph,
                self.inner.partition_leaders.clone(),
                self.inner.partition_peer_info.clone(),
            )?;
        }
```