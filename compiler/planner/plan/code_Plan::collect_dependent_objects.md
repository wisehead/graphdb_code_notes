#1.Plan::collect_dependent_objects
```
Plan::collect_dependent_objects
--Plan::Query(op) => self.collect_dependent_objects_from_query(graph_id, op),
----result.visit(op)?;
------PlanVisitor::visit
--Plan::DDL(op) => self.collect_dependent_objects_from_ddl(graph_id, op),
--Plan::StandaloneCall(op) => {
----self.collect_dependent_objects_from_standalone_call(graph_id, op)
--Plan::BackendJob(BackendJobOp::RunJob(op)) => {
----self.collect_dependent_objects_from_query(op.graph_id, &op.query_op)
--_ => Ok(DependentObjects::new(graph_id)),
```