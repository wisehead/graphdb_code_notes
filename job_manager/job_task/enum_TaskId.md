#1.enum TaskId

```rust
pub enum TaskId {
    Int(i64),           // 1. Distribute job, 2. Single host Job
    StringId(String),   // ID of Client's Query task
    Complex(IdInfoMsg), // The internal async task of computing for Query statement
}
```