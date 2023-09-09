#1.struct JobSpec

```rust
pub struct JobSpec {
    pub job_id: JobId,
    pub job_info: Arc<dyn Job>,
    // Single host job relates to partition id (A.K.A partition leader host)
    pub partition_id: Option<PartitionId>,
    // asked_host: Option<String>, // It is specified by Single host job
    pub name: Option<String>,  // The name of job
    pub desc: Option<String>,  // The description of job
    pub priority: Option<i32>, // The priority of job
}
```