#1.struct KvClient

```rust

pub struct KvClient {
    client: Arc<dyn KvClientInterface + Send + Sync + 'static>,
}

```