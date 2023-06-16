#1.struct Config

```rust
#[derive(Debug, Serialize, Deserialize)]
pub struct Config {
    pub node: NodeConfig,
    pub log: arcgraph_log::logger::LogConfig,
    pub meta: MetaConfig,
    pub tikv: TikvConfig,
    pub compiler: CompilerConfig,
    pub computing: ComputingConfig,
    pub memory_engine: MemoryEngineConfig,
    pub server: ServerConfig,
    pub session: SessionConfig,
    pub store: StoreConfig,
    pub client: ClientConfig,
    pub rocksdb: Option<RocksdbConfig>,
    pub trace: TraceConfig,
    pub raft_peer: Vec<RaftPeer>,
    pub transaction: TransactionConfig,
    pub partition_raft: Option<PartitionRaftConfig>,
    pub dml: DmlConfig,
    pub analytical: Option<AnalyticalConfig>,
    pub search_config: SearchConfig,
    pub job_manager: Option<JobManagerConfig>,
    pub raft_config: Option<RaftConfig>,
    pub balance_scheduler_config: Option<BalanceSchedulerConfig>,
    pub metrics: MetricsConfig,
    pub auth: Option<AuthConfig>,
}
```