#1.struct RaftNode

```rust
#[allow(dead_code)]
pub struct RaftNode<S: Store, R: LogStore> {
    pub graph_id: u32,
    pub partition_id: u32,
    pub host_id: u64,
    inner: RawNode<R>,
    pub peers: HashMap<u64, Option<Peer>>,
    pub rcv: mpsc::Receiver<Message>,
    pub snd: mpsc::Sender<Message>,
    store: S,
    // #[allow(dead_code)]
    // msg_tx: mpsc::Sender<MessageSender>,
    uncommitteds: HashMap<u64, ReplyChan>,
    should_quit: bool,
    seq: AtomicU64,
    last_snap_time: Instant,
    cfg: Arc<Config>,
    cluster: Cluster,
    state_role: StateRole,
    do_recovery: bool,
    unavailable_peers: HashSet<u64>,
    last_report_time: Instant,
    pre_leader_id: u64,
}
```