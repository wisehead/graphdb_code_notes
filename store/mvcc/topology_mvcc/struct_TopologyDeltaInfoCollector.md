#1.struct TopologyDeltaInfoCollector

```rust
pub struct TopologyDeltaInfoCollector {
    pub add_in_edges: EdgeMap,
    pub del_in_edges: EdgeMap,
    pub add_out_edges: EdgeMap,
    pub del_out_edges: EdgeMap,
    // Some(true) means vertex is deleted, Some(false) means vertex is created, None means no such actions or create and delete are done by self
    pub is_delete: Option<bool>,
}
```