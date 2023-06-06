#1.enum GraphDDL
```rust
#[derive(PartialEq, Eq, Debug)]
pub enum GraphDDL {
    ShowGraphs,
    CreateGraph(CreateGraph),
    DescGraph(DescGraph),
    UseGraph(UseGraph),
    ClearGraph(ClearGraph),
    DropGraph(DropGraph),
    RenameGraph(RenameGraph),
}
```