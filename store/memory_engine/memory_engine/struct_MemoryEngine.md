#1.struct MemoryEngine

```rust
pub struct MemoryEngine {
    graph_caches: DashMap<GraphId, Arc<GraphCache>>,
    index_buffers: DashMap<GraphId, Arc<IndexBuffer>>,
}
```