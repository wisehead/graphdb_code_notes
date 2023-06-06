#1.struct RenameGraphOp

```rust
#[derive(Debug, Clone, PartialEq, Eq, serde::Serialize, serde::Deserialize)]
#[allow(dead_code)]
pub struct RenameGraphOp {
    pub from_id: Option<GraphId>,
    pub to_id: Option<GraphId>,
    pub from_name: String,
    pub to_name: String,
}
```