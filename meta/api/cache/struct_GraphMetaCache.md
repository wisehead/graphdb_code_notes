#1.struct GraphMetaCache

```rust
pub struct GraphMetaCache {
    // key: /fabarta/graph/<graph id>
    pub(crate) graph: RwLock<Graph>,

    // key: /fabarta/config/<graph id>/partition/leader/<partition id>
    pub partition_id_leader_map: RwLock<HashMap<PartitionId, RaftPeerInfo>>,

    // key: /fabarta/config/<graph id>/partition/info
    pub partition_peer_info: RwLock<Vec<PartitionPeerInfo>>,

    // key: /fabarta/id/graph/<graph id>/elementTypeId
    pub(crate) graph_object_id_pool: IdPool<GraphObjectTypeId, EtcdIdSource>,
    // key: /fabarta/id/graph/<graph id>/propertyId
    pub(crate) field_id_pool: IdPool<GraphObjectTypeId, EtcdIdSource>,

    // /fabarta/graph:edgeType:currentVersion/<graph id>/<element id>
    pub edge_schemas: Arc<RwLock<SchemaMap>>,
    // /fabarta/graph:vertexType:currentVersion/<graph id>/<element id>
    pub vertex_schemas: Arc<RwLock<SchemaMap>>,

    // key: /fabarta/graph:element:index/<graph id>/<element id>/<index id>
    pub(crate) index: Arc<RwLock<IndexMap>>,

    pub edge_type_name_map: Arc<DashMap<String, GraphObjectTypeId>>,
    pub vertex_type_name_map: Arc<DashMap<String, GraphObjectTypeId>>,
    pub(crate) index_name_map: Arc<RwLock<HashMap<String, IndexData>>>,
}

```