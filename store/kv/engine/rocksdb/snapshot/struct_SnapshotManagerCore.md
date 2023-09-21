#1.struct SnapshotManagerCore

```rust
struct SnapshotManagerCore {
    // the directory to store snapshots.
    base_dir: String,

    registry: Arc<RwLock<HashMap<SnapshotKey, Vec<SnapshotEntry>>>>,
    limiter: Limiter,
    temp_sst_id: Arc<AtomicU64>,
}

```