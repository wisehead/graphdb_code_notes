#1.struct SnapshotCfFile

```rust
pub struct SnapshotCfFile {
    #[prost(string, tag = "1")]
    pub cf: ::prost::alloc::string::String,
    #[prost(uint64, tag = "2")]
    pub size: u64,
    #[prost(uint32, tag = "3")]
    pub checksum: u32,
}

```