#1.struct GraphCache

```rust
pub struct GraphCache {
    graph_id: GraphId,

    cache: RwLock<BTreeMap<VertexKey, Arc<CacheEntry>>>,
    pub(crate) vertex_lru: Cache<VertexKey, bool>,
    pub(crate) edge_lru: Cache<EdgeKey, bool>,

    vertex_memo: RwLock<VertexRangeMemo>,
    edge_memo: RwLock<EdgeRangeMemo>,

    load_status_for_types: RwLock<HashSet<(PartitionId, GraphObjectTypeId)>>,
    load_status_for_graph: AtomicU8,

    #[cfg(debug_assertions)]
    num_of_loaded_edges: AtomicU64,
}
```