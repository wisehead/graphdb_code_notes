#1.struct CfFileForRecving

```rust
struct CfFileForRecving {
    file: File,
    written_size: u64,
    write_digest: crc32fast::Hasher,
}
```