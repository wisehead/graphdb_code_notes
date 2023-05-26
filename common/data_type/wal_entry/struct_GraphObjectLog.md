#1.struct GraphObjectLog

```rust
#[derive(Clone, Serialize, Deserialize, Debug)]
pub struct GraphObjectLog {
    pub key: GraphObjectKey,
    pub schema_version: i32,
    pub property: GraphObjectProperty,
}

```