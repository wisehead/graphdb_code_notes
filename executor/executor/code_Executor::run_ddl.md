#1.Executor::run_ddl

```
Executor::run_ddl
--let session_id = query_ctx.session_id.clone();
--if Config::is_enable_transaction()
            && TransactionManager::get()
                .get_global_txn(&session_id)
                .await
                .is_some()
----TransactionManager::get()
                .commit_global_txn(&session_id)
                .await?;
--// Operator creates transactoin id and stmt_tso on-demand
--let stmt_ctx = StmtCtx::new(
            graph_id,
            0,
            0,
            l_plan.stmt_type(),
            l_plan.get_dependent_object().clone(),
        );
--let mut op = match l_plan.get_plan() {
----Plan::DDL(ddl_op) => DDLOperator::new(ddl_op, &stmt_ctx)?,
----Plan::StandaloneCall(call) => DDLOperator::new_with_standalone_call(call, &stmt_ctx)?,
----_ => panic!(),
--let mut result = op.process().await?;
```