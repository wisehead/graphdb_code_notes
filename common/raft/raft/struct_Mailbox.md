#1.struct Mailbox

```rust

/// A mailbox to send messages to a running raft node.
#[derive(Clone)]
pub struct Mailbox {
    cluster: Cluster,
    peer_id: u64,
    peers: Arc<DashMap<(u64, String), Peer>>,
    pub sender: mpsc::Sender<Message>,
    grpc_timeout: Duration,
    grpc_concurrency_limit: usize,
    grpc_breaker_threshold: u64,
    grpc_breaker_retry_interval: i64,
}
```