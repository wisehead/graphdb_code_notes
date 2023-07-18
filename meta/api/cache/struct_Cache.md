#1.struct Cache

```rust
pub(crate) struct Cache {
    // key: /fabarta/id/graphId
    pub(crate) graph_id_pool: IdPool<GraphId, EtcdIdSource>,

    pub(crate) graph_data: DashMap<GraphId, Arc<GraphMetaCache>>,
    pub(crate) graph_names: NameIdMap,

    // key: /fabarta/computing:node/<node id>
    pub(crate) nodes: DashMap<NodeId, Arc<Node>>,
    pub(crate) ddl_leader_node_id: RwLock<NodeId>,

    // key: /fabarta/id/jobId
    pub(crate) job_id_pool: IdPool<i64, EtcdIdSource>,
}
```