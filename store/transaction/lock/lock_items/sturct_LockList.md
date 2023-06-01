#1.struct LockList

```rust
#[derive(Debug, Default, Clone)]
pub struct LockList {
    pub(crate) graph: Option<GraphId>,
    pub(crate) schemas: HashSet<GraphObjectTypeId>,
}

```