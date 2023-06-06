#1.enum DataDefinition

```rust
#[derive(PartialEq, Eq, Debug)]
pub enum DataDefinition {
    GraphDDL(GraphDDL),
    VertexTypeDDL(VertexTypeDDL),
    EdgeTypeDDL(EdgeTypeDDL),
    EngineDDL(EngineDDL),
    IndexDDL(IndexDDL),
    LockDDL,
}
```