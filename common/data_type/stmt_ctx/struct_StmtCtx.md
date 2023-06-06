#1.struct StmtCtx

```rust
#[derive(Debug, Clone, serde::Serialize, serde::Deserialize)]
pub struct StmtCtx {
    pub graph_id: GraphId,
    pub txn_id: TransactionId,
    pub stmt_tso: TsoType,
    pub stmt_type: StmtType,
    pub depend_objects: DependentObjects,
}

```