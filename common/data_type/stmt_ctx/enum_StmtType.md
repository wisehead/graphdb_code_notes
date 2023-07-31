#1.enum StmtType

```rust
pub enum StmtType {
    Query,
    DDL(DdlType),
    DCL,
    DML,
    Job,
    StandAloneCall(CallType),
    ShowCommand,
    #[default]
    Others,
}
```