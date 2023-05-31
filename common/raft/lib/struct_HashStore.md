#1.struct HashStore

```rust
impl HashStore {
    pub fn new(graph_id: u32, partition_id: u32, peer_id: u64) -> Self {
        Self {
            graph_id,
            partition_id,
            peer_id,
            data: Arc::new(RwLock::new(HashMap::new())),
            current_leader_id: 0,
        }
    }
    fn _get(&self, _key: &str) -> Option<String> {
        None
    }
}
```