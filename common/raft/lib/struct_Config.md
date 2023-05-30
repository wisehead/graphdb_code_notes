#1.struct Config

```rust
#[derive(Clone)]
pub struct Config {
    pub grpc_timeout: Duration,
    pub grpc_concurrency_limit: usize,
    //GRPC failed to fuse threshold
    pub grpc_breaker_threshold: u64,
    pub grpc_breaker_retry_interval: Duration,
    //Proposal batchs
    pub proposal_batch_size: usize,
    pub proposal_batch_timeout: Duration,
    //Snapshot generation interval
    pub snapshot_interval: Duration,
    pub heartbeat: Duration,
    pub raft_cfg: tikv_raft::Config,
    pub report_status_interval: Duration,
}


```