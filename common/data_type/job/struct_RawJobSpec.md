#1.struct RawJobSpec

```rust
pub struct RawJobSpec {
    pub job_id: JobId,
    pub job_type: JobType,
    pub job_json_str: String,
    // Standalone mode job relates to partition id (A.K.A partition leader host)
    pub partition_id: Option<PartitionId>,
    pub name: Option<String>,  // The name of job
    pub desc: Option<String>,  // The description of job
    pub priority: Option<i32>, // The priority of job
}
```