#1.PlanBuilder::build_ast

```
PlanBuilder::build_ast
--let query = &statement.query;
--match query {
----Query::DataDefinition(data_definition) => {
------let ddl_op = self.build_ddl(data_definition)?;
------Ok(Plan::DDL(ddl_op))
```