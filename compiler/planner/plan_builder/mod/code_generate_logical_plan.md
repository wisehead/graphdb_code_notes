#1.generate_logical_plan

```
generate_logical_plan
--qo_context = QoContext::new_with_graph_id_and_session_id(graph_id, privileges);
--if let Some(qp_hints) = &statement.hints {
----qo_context.hint_context.add_hints(&qp_hints.hints)?;
--generate_logical_plan_with_context(statement, qo_context)
```

#2.caller

```
- generate_plan
- generate_plan_with_auth

```

#3.caller of generate_plan

```
GrpcQueryService::query
--Executor::execute
----Executor::execute_plan
```

