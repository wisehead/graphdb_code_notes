#1.struct MessageSender

```rust
struct MessageSender {
    messages: Vec<RaftMessage>,
    client: Peer,
    client_id: u64,
    chan: mpsc::Sender<Message>,
    max_retries: usize,
    timeout: Duration,
}
```