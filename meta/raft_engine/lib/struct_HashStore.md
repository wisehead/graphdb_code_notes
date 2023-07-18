#1.struct HashStore

```rust
pub(crate) struct HashStore {
    host_id: u64,
    graph_id: u32,
    partition_id: u32,
    peer_id: u64,
    data: Arc<RwLock<HashMap<String, String>>>,
    current_leader_id: u64,
}
```