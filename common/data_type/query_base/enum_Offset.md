#1.enum Offset

```rust
#[derive(Clone, Debug, PartialEq, Eq, Default, serde::Serialize, serde::Deserialize)]
pub enum Offset {
    #[allow(unused)]
    #[default]
    None,

    // offset number
    #[allow(unused)]
    Number(u32),

    // start point of scan
    #[allow(unused)]
    RawCode(Vec<u8>),

    // start point of the logical step
    // skip n(=u32) steps
    #[allow(unused)]
    SkipLogicalSteps(u32, Box<Offset>),

    // offset in topology cache
    VertexOffset(VertexKey),
    EdgeOffset(EdgeKey),

    // there's no more data in storage
    #[allow(unused)]
    End,
}
```