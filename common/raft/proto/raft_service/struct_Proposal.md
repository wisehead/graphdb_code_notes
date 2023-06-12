#1.struct Proposal

```rust
#[derive(Eq, Clone, PartialEq, ::prost::Message)]
pub struct Proposal {
    #[prost(uint32, tag = "1")]
    pub graph_id: u32,
    #[prost(uint32, tag = "2")]
    pub partition_id: u32,
    #[prost(uint64, tag = "3")]
    pub peer_id: u64,
    #[prost(bytes = "vec", tag = "4")]
    pub inner: ::prost::alloc::vec::Vec<u8>,
}
```