#1.struct Graph

```rust
pub struct Graph {
    #[serde(rename = "graphId")]
    pub id: u32,
    #[serde(rename = "graphName")]
    pub name: String,
    #[serde(rename = "charsetName")]
    pub charset: Charset,
    #[serde(rename = "collateName")]
    pub collate: Collate,
    #[serde(default = "String::new")]
    pub comment: String,
    #[serde(rename = "createTime")]
    pub create_time: Timestamp,
    #[serde(rename = "partitionNumber")]
    pub partition_number: u32,
    #[serde(rename = "replicaNumber")]
    pub replica_number: u32,
    pub status: SchemaStatus,
    #[serde(default)]
    pub version: i32,
    #[serde(skip)]
    pub previous_schema: Option<Arc<Graph>>,
}

```