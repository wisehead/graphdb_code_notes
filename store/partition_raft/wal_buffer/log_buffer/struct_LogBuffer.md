#1.struct LogBuffer
```rust
#[derive(Debug)]
pub struct LogBuffer {
    graph_id: GraphId,
    partition_id: PartitionId,
    pub(crate) start_lsn: u64, // record the start lsn
    logs: Vec<LogEntry>,       // The capacity is configured
    commit: Mutex<i32>,        // Only one thread can commit log to Raft at any time
    notify: Notify,
}

```