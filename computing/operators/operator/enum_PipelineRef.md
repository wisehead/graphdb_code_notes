#1.enum PipelineRef

```rust
pub enum PipelineRef<'a> {
    MainPipeline(&'a Pipeline),
    WorkerPipeline(&'a WorkerPipeline),
}
```
