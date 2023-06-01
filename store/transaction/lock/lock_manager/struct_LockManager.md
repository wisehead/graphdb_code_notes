#1.struct LockManager

```rust
pub struct LockManager {
    enable: bool,
    timeout: Duration,
    graph_lock_map: Mutex<HashMap<GraphId, LockRequestQueue>>,
    schema_lock_map: Mutex<HashMap<GraphObjectTypeId, LockRequestQueue>>,
}

```