#1.struct GraphMetaData

```rust
pub struct GraphMetaData {
    // key: /fabarta/graph/<graph id>
    pub graph: RwLock<Graph>,

    // key: /fabarta/config/<graph id>/partition/leader/<partition id>
    pub partition_id_leader_map: RwLock<HashMap<PartitionId, RaftPeerInfo>>,

    // key: /fabarta/config/<graph id>/partition/peer/{partition_id}/{peer_id}
    pub partition_peer_info: RwLock<Vec<PartitionPeerInfo>>,

    // /fabarta/graph:edgeType:currentVersion/<graph id>/<element id>
    pub edge_schemas: Arc<RwLock<SchemaMap>>,
    // /fabarta/graph:vertexType:currentVersion/<graph id>/<element id>
    pub vertex_schemas: Arc<RwLock<SchemaMap>>,

    // key: /fabarta/graph:element:index/<graph id>/<element id>/<index id>
    pub index: Arc<RwLock<IndexMap>>,

    pub edge_type_name_map: Arc<DashMap<String, GraphObjectTypeId>>,
    pub vertex_type_name_map: Arc<DashMap<String, GraphObjectTypeId>>,
    pub index_name_map: Arc<DashMap<String, IndexData>>,
}
```