#1.create_system_graph

```
create_system_graph
--let meta_mgr = MetaManager::get();
--let cluster = meta_mgr.get_cluster(cluster_id).expect("Cluster not exist");
--let mut partition_leaders: HashMap<PartitionId, RaftPeerInfo> = HashMap::new();
--let mut partition_peer_info: Vec<PartitionPeerInfo> = Vec::new();
--let graph = build_internal_graph().unwrap();
--update_partition_info(
        &cluster,
        &graph,
        &mut partition_leaders,
        &mut partition_peer_info,
    );
```