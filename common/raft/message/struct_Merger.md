#1.struct Merger

```rust
#[allow(dead_code)]
pub(crate) struct Merger {
    proposals: Vec<Vec<u8>>,
    chans: Vec<(Sender<RaftResponse>, Instant)>,
    start_collection_time: i64,
    proposal_batch_size: usize,
    proposal_batch_timeout: i64,
}
```