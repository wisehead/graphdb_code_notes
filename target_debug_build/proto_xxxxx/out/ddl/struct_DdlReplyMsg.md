#1.struct DdlReplyMsg

```rust
pub struct DdlReplyMsg {
    /// gRPC status
    #[prost(message, optional, tag = "1")]
    pub msg: ::core::option::Option<super::compute::ReplyMsg>,
    /// Schema information
    #[prost(message, optional, tag = "2")]
    pub schema: ::core::option::Option<super::common::DataSetMsg>,
    #[prost(bytes = "vec", tag = "3")]
    pub result: ::prost::alloc::vec::Vec<u8>,
}
```