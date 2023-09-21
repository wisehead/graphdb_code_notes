#1.struct GraphInstances

```rust
pub struct GraphInstances {
    pub graph_map: RwLock<HashMap<u32, Arc<GraphInstance>>>,
}

```