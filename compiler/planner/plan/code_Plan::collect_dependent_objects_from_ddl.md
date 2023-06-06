#1.Plan::collect_dependent_objects_from_ddl

```
Plan::collect_dependent_objects_from_ddl
--let mut schema_map = HashMap::new();
--match op {
----DDLOp::AlterVertexType(alter_op) => {
----DDLOp::DropVertexType(drop_op) => {
----DDLOp::AlterEdgeType(alter_op) => {
----DDLOp::DropEdgeType(drop_op) => {
----DDLOp::CreateIndex(create_index_op) => {
----DDLOp::DropIndex(drop_index_op) => {
----DDLOp::RebuildIndex(rebuild_index_op) => {
----_ => {}
--Ok(DependentObjects {
            graph_id,
            schema: schema_map,
        })
```