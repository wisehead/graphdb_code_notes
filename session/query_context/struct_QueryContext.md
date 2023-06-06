#1. struct QueryContext

```rust
// ERROR = 0,
// PENDING = 1,
// RUNING = 2,
// FINISH = 3,

pub struct QueryContext {
    pub session_id: String,
    pub transaction_id: String,
    pub results: Arc<ResultPool>,
    pub result_cache: Arc<RwLock<HashMap<String, Arc<ResultCache>>>>,
    pub params: Option<HashMap<String, String>>,
    pub query_msg: String,
    pub graph_id: GraphId,
    // TODO: will be changed to physic plan
    pub plan_node: Option<PlanNode>,
    pub status: Arc<AtomicI32>,
    pub number_result: i64,
    pub sender: async_channel::Sender<String>,
    pub receiver: async_channel::Receiver<String>,
    pub batchsize: i64,
    pub error_code: Arc<RwLock<Option<ErrorCode>>>,
    pub user_id: String,
    pub start: SystemTime,
    pub notify: Arc<Notify>,
    pub first_batch: AtomicBool,
    pub idle_time: Arc<parking_lot::RwLock<Instant>>,
    pub host_set: RwLock<HashSet<String>>,
    pub computing_info: Arc<RwLock<ComputingInfo>>,
}

```