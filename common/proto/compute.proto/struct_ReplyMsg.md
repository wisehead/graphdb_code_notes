#1.struct ReplyMsg

```rust
#[derive(Eq)]
#[allow(clippy::derive_partial_eq_without_eq)]
#[derive(Clone, PartialEq, ::prost::Message)]
pub struct ReplyMsg {
    #[prost(enumeration = "reply_msg::Status", tag = "1")]
    pub status: i32,
    #[prost(string, tag = "2")]
    pub msg: ::prost::alloc::string::String,
}
```