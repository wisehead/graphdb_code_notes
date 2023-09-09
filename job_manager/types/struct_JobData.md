#1.struct JobData

```rust
pub(crate) struct JobData {
    #[allow(unused)]
    pub job_spec: Arc<JobSpec>,
    pub job_status: RwLock<HashMap<String, JobStatus>>,
    retry_count: AtomicI32,
}
```