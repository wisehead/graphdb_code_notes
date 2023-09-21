#1.struct SnapshotMeta

```rust
pub struct SnapshotMeta {
    #[prost(message, repeated, tag = "1")]
    pub cf_files: ::prost::alloc::vec::Vec<SnapshotCfFile>,
}
```