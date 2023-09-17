#1.struct ClusterInfo

```rust
pub struct ClusterInfo {
    cluster_id: ClusterId,
    // key: /fabarta/computing:node/<node id>
    pub(crate) nodes: DashMap<NodeId, Arc<Node>>,

    // key: /fabarta/id/graphId
    pub(crate) graph_id_pool: IdPool<GraphId, IdSource>,
    // key: /fabarta/id/jobId
    pub(crate) job_id_pool: IdPool<JobId, IdSource>,

    pub(crate) graphs: DashMap<GraphId, Arc<GraphMetaData>>,
    pub(crate) graph_names: DashMap<String, GraphId>,
    // key: /fabarta/id/graph/<graph id>/elementTypeId
    pub(crate) graph_object_id_pools: DashMap<GraphId, Arc<IdPool<GraphObjectTypeId, IdSource>>>,
    // key: /fabarta/id/graph/<graph id>/propertyId
    pub(crate) field_id_pools: DashMap<GraphId, Arc<IdPool<GraphObjectTypeId, IdSource>>>,

    pub(crate) tso: Arc<dyn meta_tso::timestamp_oracle::TimeStampOracle>,
    pub(crate) min_read_ts_manager: MinReadTsManager,
    pub(crate) meta_store: Arc<meta_store::MetaStore>,
}
```