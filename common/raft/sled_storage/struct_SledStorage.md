#1.struct SledStorage

```rust
#[allow(dead_code)]
pub struct SledStorage {
    graph_id: u32,
    partition_id: u32,
    core: Db,
    active_txns: RefCell<HashMap<TransactionId, u64>>,
    snapshot_metadata: SnapshotMetadata,
}

```