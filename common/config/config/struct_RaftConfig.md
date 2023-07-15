#1.struct RaftConfig

```rust
#[derive(Debug, Serialize, Deserialize, Clone, Copy)]
pub struct RaftConfig {
    pub grpc_timeout: u64,
    pub grpc_concurrency_limit: usize,
    pub grpc_breaker_threshold: u64,
    pub grpc_breaker_retry_interval: u64,
    pub proposal_batch_size: usize,
    pub proposal_batch_timeout: u64,
    pub snapshot_interval: u64,
    pub heartbeat: u64,
    pub report_status_interval: u64,
    pub election_tick: usize,
    pub heartbeat_tick: usize,
    pub check_quorum: bool,
    pub pre_vote: bool,
    pub message_sender_max_retries: usize,
    pub message_sender_timeout: u64,
}
```