#1.PlanBuilder::build_graph_ddl
```
PlanBuilder::build_graph_ddl
--GraphDDL::UseGraph(q) => self.build_use_graph(q),
--GraphDDL::DescGraph(q) => self.build_desc_graph(q),
--GraphDDL::ShowGraphs => Ok(DDLOp::ShowGraphs),
--GraphDDL::ClearGraph(q) => self.build_clear_graph(q),
--GraphDDL::CreateGraph(q) => self.build_create_graph(q),
--GraphDDL::DropGraph(q) => self.build_drop_graph(q),
--GraphDDL::RenameGraph(q) => self.build_rename_graph(q),
```