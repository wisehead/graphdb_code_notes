#1.DDLValidator::validate

```
DDLValidator::validate
--DDLOp::UseGraph(op) => ddl_validator.validate_use_graph_op(op),
--DDLOp::DescGraph(op) => ddl_validator.validate_des_graph_op(op),
--DDLOp::ClearGraph(op) => ddl_validator.validate_clear_graph_op(op),
--DDLOp::CreateGraph(op) => ddl_validator.validate_create_graph_op(op),
--DDLOp::DropGraph(op) => ddl_validator.validate_drop_graph_op(op),
--DDLOp::RenameGraph(op) => ddl_validator.validate_rename_graph_op(op),
--DDLOp::CreateVertexType(op) => ddl_validator.validate_create_vertex_type_op(op),
--DDLOp::DescVertexType(op) => ddl_validator.validate_desc_vertex_type_op(op),
--DDLOp::DropVertexType(op) => ddl_validator.validate_drop_vertex_type_op(op),
--DDLOp::CreateEdgeType(op) => ddl_validator.validate_create_edge_type_op(op),
--DDLOp::AlterVertexType(op) => ddl_validator.validate_alter_vertex_type_op(op),
--DDLOp::DescEdgeType(op) => ddl_validator.validate_desc_edge_type_op(op),
--DDLOp::DropEdgeType(op) => ddl_validator.validate_drop_edge_type_op(op),
--DDLOp::AlterEdgeType(op) => ddl_validator.validate_alter_edge_type_op(op),
--DDLOp::ShowIndexes(op) => ddl_validator.validate_show_indexes_op(op),
--DDLOp::ShowIndexStatus(op) => ddl_validator.validate_show_index_status_op(op),
--DDLOp::DescIndex(op) => ddl_validator.validate_desc_index_op(op),
--DDLOp::CreateIndex(op) => ddl_validator.validate_create_index_op(op),
--DDLOp::DropIndex(op) => ddl_validator.validate_drop_index_op(op),
--DDLOp::RebuildIndex(op) => ddl_validator.validate_rebuild_index_op(op),
```