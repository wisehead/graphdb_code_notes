#1.struct LogBuffer
```rust
pub struct LogBuffer {
    // RAFT related info
    //

    // Fields used to flush log
    pub graph_id: GraphId,
    pub partition_id: PartitionId,
    pub peer_id: RaftPeerId,

    // Log buffer related info
    //

    // LogBuffer related config
    config: LogBufferConfig,

    // Used to store LogEntry in heap memory in LSN order
    logs: Vec<LogEntry>,

    // Use links to implement lock-free contiguous writable log space detection
    links: Box<LinkBuffer>,

    // Critical LSN related info
    //

    // LSNs before write_lsn have been written out already
    write_lsn: AtomicU64,

    // LSNs before flush_lsn have been flushed to raft already
    flush_lsn: AtomicU64,

    // LSNs before notify_lsn have been notified to user already
    notify_lsn: AtomicU64,

    // Log writer related info
    //

    // User task use it to wait on and notify by log writer
    // thread safe
    user_task_notify: Notify,

    // Log writer use it to wait on and notify by user force/commit flush
    // thread safe
    log_writer_notify: Notify,

    // When log writer flush raft failed, log_has_error will be set
    // and store error code in log_error_code
    log_has_error: AtomicBool,
    log_error_code: Option<ErrorCode>,
}


```