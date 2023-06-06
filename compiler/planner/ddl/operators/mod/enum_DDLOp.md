#1.enum DDLOp

```rust
#[derive(Debug, Clone, PartialEq, Eq, serde::Serialize, serde::Deserialize)]
pub enum DDLOp {
    ShowGraphs,
    UseGraph(UseGraphOp),
    CreateGraph(CreateGraphOp),
    DescGraph(DescGraphOp),
    ClearGraph(ClearGraphOp),
    DropGraph(DropGraphOp),
    RenameGraph(RenameGraphOp),
    ShowVertexTypes(ShowVertexTypesOp),
    CreateVertexType(CreateVertexTypeOp),
    DescVertexType(DescVertexTypeOp),
    AlterVertexType(AlterVertexTypeOp),
    DropVertexType(DropVertexTypeOp),
    ShowEdgeTypes(ShowEdgeTypesOp),
    CreateEdgeType(CreateEdgeTypeOp),
    DescEdgeType(DescEdgeTypeOp),
    AlterEdgeType(AlterEdgeTypeOp),
    DropEdgeType(DropEdgeTypeOp),
    ShowDDLLeader,
    ShowLocks(ShowLocksOp),
    ShowIndexes(ShowIndexesOp),
    ShowIndexStatus(ShowIndexStatusOp),
    DescIndex(DescIndexOp),
    CreateIndex(CreateIndexOp),
    DropIndex(DropIndexOp),
    RebuildIndex(RebuildIndexOp),
    Dummy,
}
```