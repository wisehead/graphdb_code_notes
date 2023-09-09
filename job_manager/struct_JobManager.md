#1.struct JobManager

```rust
pub struct JobManager {
    // job queues: DataTransfer, Doc, Ap, Other
    queues: Vec<RwLock<JobQueue>>,
    // Get Job by id
    job_id_map: RwLock<HashMap<JobId, Arc<JobData>>>,
    notify: Arc<Notify>,
}
```