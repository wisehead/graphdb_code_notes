#1.struct InsertPlan

```rust
pub struct InsertPlan {
    pub(crate) insert_vertexes: Vec<InsertVertex>,
    pub(crate) insert_edges: Vec<InsertEdge>,
    pub(crate) rel_id: PlanNodeId,
    pub(crate) output_format: OutputFormat,
}
```