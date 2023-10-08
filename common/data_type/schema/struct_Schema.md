#1.struct Schema

```rust
pub struct Schema {
    pub id: GraphObjectTypeId,
    pub name: String,
    pub version: SchemaVersion,
    pub status: SchemaStatus,
    pub comment: String,
    pub fields: Vec<Field>,
    pub field_names: Vec<String>,
    pub fields_id_map: HashMap<FieldId, Field>,
    pub fields_sequence: HashMap<String, usize>,
    pub key_length: usize,
    pub key_type: ValueType,
    pub null_bytes_size: usize,
    pub nullable_field_index: Vec<usize>,
    pub previous_schema: Option<Arc<Schema>>,
    pub vertex_type_pairs: Vec<VertexTypePair>,
    pub rankable: bool,
    pub partition_schema: PartitionSchema,
}

```