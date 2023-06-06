#1.struct SessionManager

```rust
pub struct SessionManager {
    pub session_count: i32,
    pub active_sessions: Arc<RwLock<HashMap<String, Arc<ClientSession>>>>,
    pub active_transactions: Arc<RwLock<HashMap<String, Arc<QueryContext>>>>,
    pub meta_client: Option<MetaClient>,
    pub active_sessions_transactions: Arc<RwLock<HashMap<String, String>>>,
    pub host_addr: String,
    pub local_query_cache: QueryCache,
    pub ttl: Duration,
}

```