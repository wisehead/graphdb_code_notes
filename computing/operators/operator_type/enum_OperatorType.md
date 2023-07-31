#1.enum OperatorType

```rust
#[impl_operator_type_build_methods]
pub enum OperatorType {
    Normal(NormalCore),
    LBlock(LBlockCore),
    RBlock(RBlockCore),
    SortCollectorPre(SortCollectorPreCore),
    SortCollectorPost(SortCollectorPostCore),
    TopK(TopKCore),
    UnionPre(UnionPreCore),
    UnionPost(UnionPostCore),
    DMLPre(DMLPreCore),
    DMLPost(DMLPostCore),
    DMLFinishPre(DMLFinishPreCore),
    DMLFinishPost(DMLFinishPostCore),
    GroupByPre(GroupByPreCore),
    GroupByPost(GroupByPostCore),
    IntersectPre(IntersectPreCore),
    IntersectPost(IntersectPostCore),
    ExceptPre(ExceptPreCore),
    ExceptPost(ExceptPostCore),
    JaccardPre(JaccardPreCore),
    JaccardPost(JaccardPostCore),
    ShowFullProcesslist(ShowFullProcesslistCore),
}


```