#1.struct SnapshotKey

```rust
pub struct SnapshotKey {
    pub graph_id: GraphId,
    pub partition_id: PartitionId,
    pub term: u64,
    pub index: u64,
}

```