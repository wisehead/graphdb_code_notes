#1.struct Node

```rust
#[derive(Serialize, Deserialize, Debug, Clone)]
pub struct Node {
    pub id: NodeId,
    pub name: String,
    pub ip: String,
    pub address: String,
    pub raft_address: String,
    pub label: Option<String>,
    pub node_status: Option<NodeStatus>,
    pub last_report_time: Option<u128>,
}

```