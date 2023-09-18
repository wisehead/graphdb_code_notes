#1.struct ReplyMsg

```rust
pub struct ReplyMsg {
    #[prost(enumeration = "super::common::ReplyStatus", tag = "1")]
    pub status: i32,
    #[prost(string, tag = "2")]
    pub msg: ::prost::alloc::string::String,
    #[prost(bytes = "vec", optional, tag = "3")]
    pub ret_data: ::core::option::Option<::prost::alloc::vec::Vec<u8>>,
}
```