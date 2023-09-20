#1.DDLOperator::process_with_step

```
DDLOperator::process_with_step
--match step {
----s if s == DdlStep::KStepForward as i32 => self.inner.process(&self.stmt_ctx).await,
----s if s == DdlStep::KStepPrepare as i32 => {
                let result = self.inner.prepare(&self.stmt_ctx, is_meta_leader).await;
                if result.is_err() {
                    let _ = self.inner.rollback(&self.stmt_ctx, is_meta_leader).await;
                }
                result
            }
----s if s == DdlStep::KStepCleanup as i32 => {
                self.inner.cleanup(&self.stmt_ctx, is_meta_leader).await
            }
----s if s == DdlStep::KStepRollback as i32 => {
                self.inner.rollback(&self.stmt_ctx, is_meta_leader).await
            }
----_ => Err(ErrorCode::UnImplement(format!(
                "Invalid DDL Action Request {}",
                step
            ))),
        }
```