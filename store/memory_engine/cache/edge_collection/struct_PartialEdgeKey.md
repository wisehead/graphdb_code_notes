#1.struct PartialEdgeKey

```rust
pub struct PartialEdgeKey {
    pub dst_vertex_key: VertexKey,
    pub type_id: u32,
    pub direction: EdgeDirection,
    pub rank: Rank,
}

```