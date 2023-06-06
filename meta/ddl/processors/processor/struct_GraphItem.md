#1.struct GraphItem

```rust
#[derive(Clone, Debug, Default)]
pub struct GraphItem {
    pub graph_id: GraphId,
    pub graph_name: String,
    pub vertex_name: Vec<String>,
    pub edge_name: Vec<String>,
    pub index_name: Vec<String>,
}
```