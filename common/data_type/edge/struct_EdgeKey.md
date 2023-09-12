#1.struct EdgeKey

```rust
pub struct EdgeKey {
    // from vertex
    pub src_vertex_key: VertexKey,
    // to vertex
    pub dst_vertex_key: VertexKey,
    pub type_id: u32,
    // if edge direction is in, then it means (src_vertex_key <- dst_vertex_key)
    pub direction: EdgeDirection,
    pub rank: Rank,
}
```