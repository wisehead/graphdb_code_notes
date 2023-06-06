#1.struct PlanBuilder

```rust
pub struct PlanBuilder<'a> {
    pub qo_context: &'a mut QoContext,
    next_anonymous_id: u32,
    paths: Vec<PathExpr>,
}

```