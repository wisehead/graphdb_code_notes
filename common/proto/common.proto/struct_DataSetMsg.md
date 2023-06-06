#1.struct DataSetMsg

```rust

#[allow(clippy::derive_partial_eq_without_eq)]
#[derive(Clone, PartialEq, ::prost::Message)]
pub struct DataSetMs {
    #[prost(string, repeated, tag = "1")]
    pub header: ::prost::alloc::vec::Vec<::prost::alloc::string::String>,
    #[prost(message, repeated, tag = "2")]
    pub row: ::prost::alloc::vec::Vec<ArrayMsg>,
    #[prost(int32, repeated, tag = "3")]
    pub count: ::prost::alloc::vec::Vec<i32>,
}
```