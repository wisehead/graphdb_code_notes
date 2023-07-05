#1.struct Plan

```rust
pub struct Plan {
    id: i64,
    graph_id: u32,
    blocks: Vec<Block>,
    block_idx: HashMap<i64, usize>,
    pipelines: HashMap<i64, Arc<Pipeline>>,
    cur_block_idx: AtomicUsize,
    ctx_id: String,
    request_id: u64,
    first_batch: AtomicBool,
    pre_post_op_rels: HashMap<i64, OperatorInfo>,
    stmt_ctx: Arc<StmtCtx>,
    auto_commit: bool,
}
```