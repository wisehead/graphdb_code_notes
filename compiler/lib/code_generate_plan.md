#1.generate_plan

```
generate_plan
--let ast_plan = parser::parse(cql_input)?;
--planner::generate_logical_plan(&ast_plan, graph_id)
```

#2.caller

Executor::execute_plan
