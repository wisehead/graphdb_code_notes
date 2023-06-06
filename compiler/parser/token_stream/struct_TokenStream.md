#1.struct TokenStream

```rust
#[derive(Debug, Clone)]
pub struct TokenStream<'a> {
    pub tokens: VecDeque<Token<'a>>,
    pub error: &'a RefCell<Option<ParserError<'a>>>,
}

```