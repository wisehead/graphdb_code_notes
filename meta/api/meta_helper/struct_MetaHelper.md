#1.struct MetaHelper

```rust
pub struct MetaHelper {
    pub node: Node,
    pub meta_client: MetaClient,
    pub unregister_ts_list: crossbeam_skiplist::SkipSet<TransactionTs>,
    pub last_unregister_time: RwLock<Instant>,
    pub cache: Cache,
}
```