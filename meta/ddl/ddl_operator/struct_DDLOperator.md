#1.struct DDLOperator

```rust
pub struct DDLOperator {
    inner: Box<dyn Processor>,
    stmt_ctx: StmtCtx,
}
```