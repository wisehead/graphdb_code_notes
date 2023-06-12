#1.enum RaftResponse

```rust
#[allow(dead_code)]
pub enum Message {
    Propose {
        proposal: Vec<u8>,
        chan: Sender<RaftResponse>,
    },
    Query {
        query: Vec<u8>,
        chan: Sender<RaftResponse>,
    },
    ConfigChange {
        cluster: Cluster,
        peer_id: u64,
        change: ConfChange,
        chan: Sender<RaftResponse>,
    },
    RequestId {
        chan: Sender<RaftResponse>,
    },
    ReportUnreachable {
        node_id: u64,
    },
    Raft(Box<RaftMessage>),
    Status {
        chan: Sender<RaftResponse>,
    },
    Checkpoint {
        chan: Sender<RaftResponse>,
    },
    TransferLeader {
        transferee: u64,
        chan: Sender<RaftResponse>,
    },
}
```