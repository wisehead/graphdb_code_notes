#1.struct LockRequest

```rust
#[derive(Debug)]
pub struct LockRequest {
    txn_id: TransactionId,
    lock_mode: LockMode,
}
```