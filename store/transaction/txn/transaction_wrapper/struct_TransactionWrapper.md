#1.struct TransactionWrapper

```rust
pub struct TransactionWrapper {
    pub(crate) txn: RwLock<Transaction>,
}
```