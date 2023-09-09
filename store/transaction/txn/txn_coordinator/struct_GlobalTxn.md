#1.struct GlobalTxn

```rust
pub struct GlobalTxn {
    pub(crate) txn_id: TransactionId,
    pub(crate) graph_id: GraphId,
    pub(crate) txn_type: TransactionType,
}
```