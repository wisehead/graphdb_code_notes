#1.struct NodeInfoMsg

```rust
struct NodeInfoMsg {
    #[prost(string, tag = "1")]
    pub name: ::prost::alloc::string::String,
    #[prost(string, tag = "2")]
    pub ip_address: ::prost::alloc::string::String,
    #[prost(uint32, tag = "3")]
    pub node_id: u32,
    #[prost(uint32, tag = "4")]
    pub cluster_id: u32,
    #[prost(uint32, tag = "5")]
    pub port: u32,
    #[prost(uint32, tag = "6")]
    pub raft_port: u32,
    #[prost(enumeration = "NodeStatus", tag = "7")]
    pub node_status: i32,
    #[prost(string, tag = "8")]
    pub label: ::prost::alloc::string::String,
    #[prost(string, tag = "9")]
    pub last_report_time: ::prost::alloc::string::String,
    #[prost(int32, tag = "10")]
    pub node_type: i32,
}
```