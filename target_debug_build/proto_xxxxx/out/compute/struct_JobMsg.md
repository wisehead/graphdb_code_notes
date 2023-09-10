#1.struct JobMsg

```rust
pub struct JobMsg {
    #[prost(enumeration = "JobAction", tag = "1")]
    pub action: i32,
    /// JobSpec
    #[prost(bytes = "vec", tag = "2")]
    pub job_spec: ::prost::alloc::vec::Vec<u8>,
}

```