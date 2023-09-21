#1.struct SnapshotData

```rust
pub struct SnapshotData {
    #[prost(uint64, tag = "1")]
    pub file_size: u64,
    #[prost(uint64, tag = "2")]
    pub version: u64,
    #[prost(message, optional, tag = "3")]
    pub meta: ::core::option::Option<SnapshotMeta>,
}

```