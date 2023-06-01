#1.struct LockRequestQueue

```rust
#[derive(Debug)]
pub struct LockRequestQueue {
    queue: VecDeque<LockRequest>,
    notify: Arc<Notify>,
}
```