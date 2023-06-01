#1.struct Transaction

```rust
#[derive(Debug)]
pub struct Transaction {
    pub(crate) txn_id: TransactionId,
    pub(crate) graph_id: GraphId,
    pub(crate) commit_ts: TransactionTs,
    pub(crate) txn_state: TransactionState,
    pub(crate) modified_partitions: HashSet<PartitionId>,
    pub(crate) acquired_locks: LockList,
    pub(crate) modifies: MvccCollector,
    pub(crate) txn_type: TransactionType,
}
```