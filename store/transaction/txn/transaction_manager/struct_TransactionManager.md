#1.struct TransactionManager

```rust
pub struct TransactionManager {
    pub(crate) txn_map: RwLock<BTreeMap<TransactionId, Arc<TransactionWrapper>>>,
    pub(crate) non_txn_map: RwLock<BTreeMap<GraphId, Arc<NonTransactionWrapper>>>,
    pub(crate) global_txn_map: RwLock<HashMap<String, (TransactionId, GraphId)>>,
    pub(crate) gc_timeout: u64,
}

```