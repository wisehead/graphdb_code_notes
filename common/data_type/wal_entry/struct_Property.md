#1.struct Property

```rust
#[derive(Clone, Serialize, Deserialize, Debug)]
pub struct Property {
    pub id: FieldId,
    pub value: Value,
}
```