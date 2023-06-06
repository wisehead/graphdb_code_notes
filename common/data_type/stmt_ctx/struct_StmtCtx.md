#1.struct StmtCtx

```rust
#[derive(Debug, Clone, serde::Serialize, serde::Deserialize)]
pub enum StmtType {
    Query,
    DDL(DdlType),
    DCL,
    DML,
    Job,
    StandAloneCall(CallType),
    Others,
}
```