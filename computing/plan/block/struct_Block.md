#1.struct Block

```rust
pub struct Block {
    id: i64,
    plan_id: i64,
    pipelines: Vec<i64>,
    pipe_cnt: AtomicU8,
    processed: AtomicBool,
}
```