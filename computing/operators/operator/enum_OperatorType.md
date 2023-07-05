#1.enum OperatorType

```rust
pub enum OperatorType {
    #[default]
    Normal = 1,
    LBlock = 2,
    RBlock = 3,
    SortCollectorPre = 4,
    SortCollectorPost = 5,
    TopK = 6,
    UnionPre = 7,
    UnionPost = 8,
    DMLPre = 9,
    DMLPost = 10,
    DMLFinishPre = 11,
    DMLFinishPost = 12,
    GroupByPre = 13,
    GroupByPost = 14,
    IntersectPre = 15,
    IntersectPost = 16,
    ExceptPre = 17,
    ExceptPost = 18,
    JaccardPre = 19,
    JaccardPost = 20,
}

```