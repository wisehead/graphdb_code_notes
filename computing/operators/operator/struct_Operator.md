#1.struct Operator

```rust
pub struct Operator {
    op_info: OperatorInfo,
    is_running: Arc<AtomicBool>,
    op_type: OperatorType,
    processor: Box<dyn Processor>,
    next_op_id: Option<i64>,
    plan_node: Arc<PlanNode>,
    output_target: OutputTarget,
    has_input: bool,
}

```