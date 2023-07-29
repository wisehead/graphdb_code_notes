#1.struct RaftPeerStatus

```rust
impl RaftPeerStatus {
    pub fn key(&self) -> String {
        format!(
            "{}{}{}{}/{}",
            K_CONFIG_PREFIX,
            self.graph_id,
            K_CONFIG_PARTITION_PEER_STATUS,
            self.partition_id,
            self.peer_id
        )
    }
}
```