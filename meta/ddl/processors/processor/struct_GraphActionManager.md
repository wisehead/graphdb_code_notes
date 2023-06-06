#1.struct GraphActionManager

```rust
struct GraphActionManager {
    graph_name: RwLock<HashSet<String>>,
    vertex_name: RwLock<HashSet<String>>,
    edge_name: RwLock<HashSet<String>>,
    index_name: RwLock<HashSet<String>>,
}

```