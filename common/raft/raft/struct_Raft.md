#1.struct Raft

```rust
pub struct Raft<S: Store + 'static, R: LogStore + 'static> {
    graph_id: u32,
    partition_id: u32,
    host_id: u64,
    store: S,
    storage: R,
    tx: mpsc::Sender<Message>,
    rx: mpsc::Receiver<Message>,
    addr: String,
    logger: slog::Logger,
    cfg: Arc<Config>,
    cluster: Cluster,
    do_recovery: bool,
}

```