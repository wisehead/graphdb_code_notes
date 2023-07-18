#1.enum Message

```rust
pub enum Message {
    Insert { key: String, value: String },
    Get { key: String },
}

```