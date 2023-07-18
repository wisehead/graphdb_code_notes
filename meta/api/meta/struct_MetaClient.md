#1.struct MetaClient

```rust
pub struct MetaClient {
    pub node: Node,
    pub etcd_client: Client,
    lease_ttl: Option<i64>,
    pub unregister_ts_list: crossbeam_skiplist::SkipSet<TransactionTs>,
    pub last_unregister_time: RwLock<Instant>,
    pub(crate) cache: Cache,
}
```