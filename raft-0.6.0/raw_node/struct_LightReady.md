#1.struct LightReady

```rust
/// LightReady encapsulates the commit index, committed entries and
/// messages that are ready to be applied or be sent to other peers.
#[derive(Default, Debug, PartialEq)]
pub struct LightReady {
    commit_index: Option<u64>,
    committed_entries: Vec<Entry>,
    messages: Vec<Message>,
}

```