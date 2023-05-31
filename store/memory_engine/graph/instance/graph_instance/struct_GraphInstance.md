#1.struct GraphInstance

```rust
pub struct GraphInstance {
    pub id: u32,
    pub vertex_schema_map: Arc<RwLock<SchemaMap>>,
    pub edge_schema_map: Arc<RwLock<SchemaMap>>,
    pub kv_client: Arc<KvClient>,
    pub vertex_type_name_map: Arc<RwLock<HashMap<String, u32>>>,
    pub edge_type_name_map: Arc<RwLock<HashMap<String, u32>>>,
    pub vertex_query_processor: Arc<VertexQueryProcessor>,
    pub edge_query_processor: Arc<EdgeQueryProcessor>,
    pub(crate) _schema_processor: Arc<SchemaProcessor>,
}

```