#1.struct QueryOp

```rust
pub struct QueryOp {
    pub plan_node: Box<PlanNode>,
    // Generally most of the PlanNodes only contain one or two or none children,
    // but for future usage, we keep the extensibility with Vec.
    pub children: Vec<Box<QueryOp>>,
}
```