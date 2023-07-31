#1.struct ProcessContext

```rust
pub struct ProcessContext<'a> {
    pub plan_node: Arc<PlanNode>,
    pub op_info: &'a OperatorInfo,
    pub next_op_id: &'a Option<i64>,
    pub pipeline: PipelineRef<'a>,
    pub is_running: Arc<AtomicBool>,
    pub tracker: Arc<ProcessTracker>,
}
```