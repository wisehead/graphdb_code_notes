#1.struct MvccCollector

```rust
#[derive(Debug, Default)]
pub struct MvccCollector {
    pub edges: HashMap<EdgeKey, (PropertyMain, Arc<PropertyUndoDelta>, bool)>,
    pub vertexes: HashMap<VertexKey, (PropertyMain, Arc<PropertyUndoDelta>, bool)>,

    graph_id: GraphId,
    is_committed: Arc<AtomicBool>,
    processing_edges: HashMap<EdgeKey, (PropertyMain, PropertyUndoDelta)>,
    processing_vertexes: HashMap<VertexKey, (PropertyMain, PropertyUndoDelta)>,
    topology: HashMap<VertexKey, (DoublyLinkedList<TopologyDelta>, bool)>,

    index_buffer: IndexBufferInTrans,
}

```