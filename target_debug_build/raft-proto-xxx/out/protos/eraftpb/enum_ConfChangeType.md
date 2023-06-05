#1.enum ConfChangeType

```rust
#[derive(Clone,PartialEq,Eq,Debug,Hash)]
pub enum ConfChangeType {
    AddNode = 0,
    RemoveNode = 1,
    AddLearnerNode = 2,
}

```