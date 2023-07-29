#1.struct RaftPeerInfo

```rust
pub struct RaftPeerInfo {
    pub node_id: NodeId,
    pub peer_id: RaftPeerId,
    pub peer_role: Option<PeerRole>,
}
```