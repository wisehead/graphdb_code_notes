#1.struct ClientSession

```rust
#[derive(Clone)]
pub struct ClientSession {
    session_id: String,
    session_key: SessionKey,
    graph_id: RefCell<GraphId>,
    life_duration: DurationTimer,
    query_ctxs: Arc<RwLock<HashMap<String, Arc<QueryContext>>>>,
    auto_commit: Cell<bool>,
    isolation_level: RefCell<IsolationLevel>,
}


```