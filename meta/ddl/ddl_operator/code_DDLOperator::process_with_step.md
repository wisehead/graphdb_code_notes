#1.DDLOperator::process_with_step

```
DDLOperator::process_with_step
--match step {
----s if s == DdlStep::KStepPrepare as i32 => {
------let result = self.inner.prepare(&self.stmt_ctx).await;
```