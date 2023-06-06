#1.struct Statement

```rust
#[derive(PartialEq, Eq, Debug)]
pub struct Statement {
    pub query: Query,
    pub hints: Option<QpHints>,
}

```