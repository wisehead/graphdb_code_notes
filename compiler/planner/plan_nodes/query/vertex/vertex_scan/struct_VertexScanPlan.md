#1.struct VertexScanPlan

```rust
pub struct VertexScanPlan {
    pub(crate) base: BasePlan,
    pub(crate) vertex_alias: String,
    pub(crate) vertex_labels: Vec<String>,
    vertex_type_ids: Vec<u32>,
    pub(crate) filter: Expression,
    pub(crate) lookup_vertex_key: Option<VertexKey>,
}

```