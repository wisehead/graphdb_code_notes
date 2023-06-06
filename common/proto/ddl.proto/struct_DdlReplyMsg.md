#1.struct DdlReplyMsg

```rust
#[allow(clippy::derive_partial_eq_without_eq)]
#[derive(Clone, PartialEq, ::prost::Message)]
pub struct DdlReplyMsg {
    /// gRPC status
    #[prost(message, optional, tag = "1")]
    pub msg: ::core::option::Option<super::compute::ReplyMsg>,
    /// Schema information
    #[prost(message, optional, tag = "2")]
    pub schema: ::core::option::Option<super::common::DataSetMsg>,
}
```

```
message DDLReplyMsg {
  // gRPC status
  compute.ReplyMsg   msg    = 1;
  // Schema information
  common.DataSetMsg  schema = 2;
}
```