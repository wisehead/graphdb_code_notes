#1.struct VertexKey

```rust
pub struct VertexKey {
    pub id: Id,
    pub id_length: usize,
    pub partition_id: u32,
    pub type_id: u32,
    pub rank: Option<Rank>,
    pub graph_id: GraphId,
}
```