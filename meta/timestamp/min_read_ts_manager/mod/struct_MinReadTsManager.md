#1.struct MinReadTsManager

```rust
pub struct MinReadTsManager {
    active_ts: SkipSet<TransactionTs>,
    etcd_client: etcd_client::Client,
}
```