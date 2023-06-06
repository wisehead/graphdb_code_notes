#1.struct DdlActionRequest

```rust
#[derive(Eq)]
#[allow(clippy::derive_partial_eq_without_eq)]
#[derive(Clone, PartialEq, ::prost::Message)]
pub struct DdlActionRequest {
    #[prost(enumeration = "DdlStep", tag = "1")]
    pub step: i32,
    #[prost(enumeration = "DdlActionType", tag = "2")]
    pub action_type: i32,
    #[prost(enumeration = "DdlItemType", tag = "3")]
    pub item_type: i32,
    #[prost(bytes = "vec", tag = "4")]
    pub msg: ::prost::alloc::vec::Vec<u8>,
    #[prost(bytes = "vec", tag = "5")]
    pub stmt_ctx: ::prost::alloc::vec::Vec<u8>,
}
```