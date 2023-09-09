#1.struct JobTask

```rust
pub struct JobTask {
    pub job_id: JobId,
    pub job: Arc<dyn Job>,
}
```