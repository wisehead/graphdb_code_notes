#1.struct PlanCtx

```rust
#[derive(Debug, Clone)]
pub struct PlanCtx {
    pub(crate) plan: Plan,
    pub(crate) dependent_objects: DependentObjects,
}
```