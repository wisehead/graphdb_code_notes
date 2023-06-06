#1.Executor::execute_plan

```
Executor::execute_plan
--let cache = SessionManager::get_instance().get_local_query_cache();
--match cache.get_and_validate(
            &query_ctx.get_user_id(),
            graph_id,
            &query_ctx.get_query_msg(),
        )
----Some(cache_l_plan) => {
------l_plan = cache_l_plan;
----None => {
------l_plan = generate_plan(&query_ctx.get_query_msg(), query_ctx.get_graph_id())?;
--match l_plan.get_plan() {
----Plan::Query(l_plan_node) => {
------Self::run_query
----Plan::Explain(l_plan_node) => {
------let plan_info = PlanInfoBuilder::build(l_plan_node);
------let msg: DataSetMsg = plan_info.into();
------query_ctx.put_explain_results(msg).await;
----Plan::DDL(_) => {
------Self::run_ddl(graph_id, &l_plan, query_ctx.clone()).await?;
----Plan::StandaloneCall(call) => 
------match call {
--------StandaloneCallOp::CloneGraphSchemaOp(_)
                | StandaloneCallOp::ShowStatisticOp(_)
                | StandaloneCallOp::UpdateStatisticOp(_) => {
----------Self::run_ddl(graph_id, &l_plan, query_ctx.clone()).await?
                }
--------StandaloneCallOp::LoadGraph(_) => {
----------Self::run_ddl(graph_id, &l_plan, query_ctx.clone()).await?
                }
--------StandaloneCallOp::BalanceLeaderOp => {
----Plan::DCL(dcl_op) => {
------Self::handle_dcl_op(
----Plan::Transaction(TransactionOp::StartTransaction) => {
------Self::start_transaction(session, query_ctx).await?;
----Plan::Transaction(TransactionOp::CommitTransaction(_)) => {
------commit_global_txn
------session.set_auto_commit(true);
----Plan::Transaction(TransactionOp::RollbackTransaction(_)) => {
------let ret = TransactionManager::get()
                    .rollback_global_txn(&session_id)
                    .await;
------session.set_auto_commit(true);
----Plan::Transaction(TransactionOp::SetIsolationLevel(level)) => {
------Self::set_isolation_level(session, level, query_ctx).await?;
----_ => {}
```

#2.caller

```
Executor::execute
--Executor::execute_plan
```

#3.caller of Executor::execute

```
- GrpcQueryService::query
// common/proto/query.proto
```