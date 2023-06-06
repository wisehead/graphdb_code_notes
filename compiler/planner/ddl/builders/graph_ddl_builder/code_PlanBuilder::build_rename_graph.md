#1.PlanBuilder::build_rename_graph

```
PlanBuilder::build_rename_graph
--let from_id = self.qo_context.get_graph_id_by_name(&ast.from_name);
--//check whether there is the same target graph name
--let to_id = self.qo_context.get_graph_id_by_name(&ast.to_name);
--Ok(DDLOp::RenameGraph(RenameGraphOp {
            from_id,
            to_id,
            from_name: ast.from_name.clone(),
            to_name: ast.to_name.clone(),
        }))
```