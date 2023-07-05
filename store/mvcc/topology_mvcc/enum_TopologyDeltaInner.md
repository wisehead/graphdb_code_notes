#1.enum TopologyDeltaInner

```rust
pub enum TopologyDeltaInner {
    InsertVertex,
    DeleteVertex,
    InsertInEdge(EdgeTypeId, VertexAndRank),
    DeleteInEdge(EdgeTypeId, VertexAndRank),
    InsertOutEdge(EdgeTypeId, VertexAndRank),
    DeleteOutEdge(EdgeTypeId, VertexAndRank),
}
```