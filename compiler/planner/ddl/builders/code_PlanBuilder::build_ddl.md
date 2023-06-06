#1.PlanBuilder::build_ddl

```
PlanBuilder::build_ddl
--DataDefinition::GraphDDL(d) => self.build_graph_ddl(d),
--DataDefinition::VertexTypeDDL(d) => self.build_vertex_type_ddl(d),
--DataDefinition::EdgeTypeDDL(d) => self.build_edge_type_ddl(d),
--DataDefinition::EngineDDL(d) => self.build_engine_ddl(d),
--DataDefinition::LockDDL => self.build_locks_ddl(),
--DataDefinition::IndexDDL(d) => self.build_index_ddl(d),
```