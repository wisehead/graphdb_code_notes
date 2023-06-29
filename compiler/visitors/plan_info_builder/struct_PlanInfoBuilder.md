#1.struct PlanInfoBuilder

```rust
pub struct PlanInfoBuilder {
    node_infos: Vec<PlanNodeInfo>,
    indents: Vec<u32>,
    curr_indent: u32,
}
```