#1.struct SnapshotManager

```rust
pub struct SnapshotManager {
    core: SnapshotManagerCore,
    max_total_size: AtomicU64,
}
```