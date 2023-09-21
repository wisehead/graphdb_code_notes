#1.struct CacheEntry

```rust
pub struct CacheEntry {
    edges: RwLock<EdgeCollection>,
    mvcc_data: RwLock<Option<Box<MvccData>>>,
}

```