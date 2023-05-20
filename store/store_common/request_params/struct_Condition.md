#1.struct Condition

```rust
#[derive(Clone, Debug, Default, serde::Serialize, serde::Deserialize)]
pub struct Condition {
    pub fields: ProjectionFields,
    pub order_by: Vec<OrderBy>,
    pub limit: Limit,
    pub offset: Offset,
    pub expression: Option<Expression>,
}


```