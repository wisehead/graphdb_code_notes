#1.struct BatchVertexParam

```rust
pub struct BatchVertexParam {
    pub keys: HashSet<VertexKey>,
    // api caller must make sure all types has needed field in condition when type_id is none
    pub type_id: Option<GraphObjectTypeId>,
    pub condition: Condition,
}

```