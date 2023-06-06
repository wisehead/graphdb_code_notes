#1.generate_logical_plan_with_context

```
generate_logical_plan_with_context
--let mut plan = plan_builder::convert_ast_to_plan(statement, &mut qo_context)?;
--let mut optimize = |plan: &mut QueryOp| -> Result<()> {
--match &mut plan {
----Plan::Query(query) => optimize(query)?,
----Plan::DDL(ddl_op) => DDLValidator::validate(ddl_op, &mut qo_context)?,
----Plan::Explain(query) => optimize(query)?,
----Plan::StandaloneCall(call) => CallValidator::validate(call, &mut qo_context)?,
----Plan::Transaction(_) => (),
----Plan::BackendJob(BackendJobOp::RunJob(r)) => optimize(&mut r.query_op)?,
----Plan::BackendJob(_) => (),
----Plan::DCL(dcl_op) => match dcl_op {
            DCLOp::DropUser(query) => optimize(query)?,
            DCLOp::AlterUser(query) => optimize(query)?,
            DCLOp::DropRole(query) => optimize(query)?,
            DCLOp::RenameRole(query) => optimize(query)?,
            DCLOp::ShowUsers(query) => optimize(query)?,
            _ => (),
        },
    }
--let objects = plan.collect_dependent_objects(qo_context.get_graph_id())?;
--Ok(PlanCtx::new(plan, objects))
```