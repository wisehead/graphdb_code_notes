#1.struct Peer

```rust
#[derive(Clone)]
pub struct Peer {
    pub addr: String,
    client: Arc<RwLock<Option<RaftGrpcClient>>>,
    grpc_fails: Arc<AtomicU64>,
    grpc_fail_time: Arc<AtomicI64>,
    crw_timeout: Duration,
    concurrency_limit: usize,
    grpc_breaker_threshold: u64,
    grpc_breaker_retry_interval: i64,
    active_tasks: Arc<AtomicI64>,
    cluster: Cluster,
    peer_id: u64,
    host_id: u64,
    peer_role: PeerRole,
}

```