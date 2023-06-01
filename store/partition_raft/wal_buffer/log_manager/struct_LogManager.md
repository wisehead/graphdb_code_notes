#1.struct LogManager

```rust
pub struct LogManager {
    buffer_map: RwLock<HashMap<String, Arc<AtomicPtr<LogBuffer>>>>,
    lsn_map: RwLock<HashMap<String, AtomicU64>>,
}
```