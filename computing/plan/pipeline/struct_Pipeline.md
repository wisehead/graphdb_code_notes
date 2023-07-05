#1.struct Pipeline

```rust
pub struct Pipeline {
    id: i64,
    graph_id: u32,
    plan_id: i64,
    request_id: u64,
    operators: Vec<Operator>,
    oper_idx_map: HashMap<i64, usize>,
    active_cnt: AtomicU16,
    is_finished: bool,
    block_id: i64,
    writing: AtomicUsize,
    pipe_type: PipeType,
}

```