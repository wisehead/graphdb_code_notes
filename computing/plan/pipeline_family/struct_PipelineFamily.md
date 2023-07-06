#1.struct PipelineFamily

```rust
pub struct PipelineFamily {
    id: i64,
    main_pipeline: Box<WorkerPipeline>,
    sub_pipelines: HashMap<i64, Box<WorkerPipeline>>,
    stmt_ctx: Arc<StmtCtx>,
    block_index: i32,
    notify: Arc<Notify>,
}
```