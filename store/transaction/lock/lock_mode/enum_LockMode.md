#1.enum LockMode
```rust
#[derive(Clone, Copy, Debug, PartialEq, Eq)]
pub enum LockMode {
    IS,
    IX,
    S,
    SIX,
    X,
}
```