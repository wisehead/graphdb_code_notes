#1.struct JobQueue

```rust
pub(crate) struct JobQueue {
    group: JobGroup,
    priority: i32,
    retry_times: i32,
    max_run_jobs: usize,
    pending_jobs: VecDeque<JobId>,
    running_jobs: HashSet<JobId>,
    cancelled_jobs: HashSet<JobId>,
}
```