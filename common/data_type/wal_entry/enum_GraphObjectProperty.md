#1.enum GraphObjectProperty

```
#[derive(Clone, Serialize, Deserialize, Debug)]
pub enum GraphObjectProperty {
    Insert(Vec<Value>),
    Delete,
    Update(Vec<Property>),
}
```