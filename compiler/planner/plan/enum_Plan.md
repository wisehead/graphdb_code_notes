#1.enum Plan

```rust
/// Plan handle
#[derive(Debug, Clone, PartialEq, Eq, serde::Serialize, serde::Deserialize)]
pub enum Plan {
    Query(QueryOp),
    DDL(DDLOp),
    DCL(DCLOp),
    Explain(QueryOp),
    Transaction(TransactionOp),
    BackendJob(BackendJobOp),
    StandaloneCall(StandaloneCallOp),
}

```