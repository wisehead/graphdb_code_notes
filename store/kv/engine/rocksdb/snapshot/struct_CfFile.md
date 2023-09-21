#1.struct CfFile

```rust
pub struct CfFile {
    pub cf: CfName,
    pub path: PathBuf,
    pub tmp_path: PathBuf,
    pub clone_path: PathBuf,
    file_for_sending: Option<Box<dyn Read + Send>>,
    file_for_recving: Option<CfFileForRecving>,
    pub kv_count: u64,
    pub size: u64,
    pub checksum: u32,
}
```