#1.struct MvccData
```rust
struct MvccData {
    vertex_mvcc: Option<MvccPropertyEntry>,
    edges_mvcc: HashMap<PartialEdgeKey, Arc<EdgeEntry>>,
}
```