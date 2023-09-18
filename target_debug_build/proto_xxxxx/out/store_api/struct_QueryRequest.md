#1.struct QueryRequest

```rust
pub struct QueryRequest {
    #[prost(enumeration = "ActionType", tag = "1")]
    pub action_type: i32,
    #[prost(bytes = "vec", tag = "2")]
    pub param: ::prost::alloc::vec::Vec<u8>,
    #[prost(bytes = "vec", tag = "3")]
    pub stmt_ctx: ::prost::alloc::vec::Vec<u8>,
}
```