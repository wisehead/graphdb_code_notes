#1.enum Value

```rust
#[derive(Clone, Debug, PartialEq, Serialize, Deserialize, Default)]
pub enum Value {
    #[default]
    None,
    Byte(u8),
    Boolean(bool),
    Int64(i64),
    Int32(i32),
    UInt64(u64),
    UInt32(u32),
    Float(f32),
    Double(f64),
    String(String),
    Timestamp(u64),
    Vector(Vec<Value>),
    VertexKey(VertexKey),
    Vertex(Vertex),
    EdgeKey(EdgeKey),
    Edge(Edge),
    Path(Path),
    PathWithProperty(PathWithProperty),
    Text(String),
    Uuid(UuidValue),
    Blob(BlobValue),
}

```