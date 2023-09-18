#1.struct MetaManager

```rust
pub struct MetaManager {
    pub meta_node: Node,
    pub meta_store: Arc<meta_store::MetaStore>,
    pub(crate) meta_nodes: DashMap<NodeId, Arc<Node>>,
    pub(crate) meta_leader: RwLock<NodeId>,
    pub(crate) clusters: DashMap<ClusterId, Arc<ClusterInfo>>,
}
```