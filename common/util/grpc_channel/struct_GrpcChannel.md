#1.struct GrpcChannel

```rust
pub struct GrpcChannel {
    channels: ChannelMap,
    pub connection_cache_ttl: AtomicU64,
    pub connect_retry: AtomicI32,
    pub connect_timeout: AtomicU64,
    pub concurrency_limit: AtomicUsize,
}
```