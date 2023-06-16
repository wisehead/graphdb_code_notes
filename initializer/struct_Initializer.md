#1.struct Initializer

```rust
pub struct Initializer {
    config: Arc<Config>,
    log_guard: Option<&'static arcgraph_log::logger::LogGuard>,
}

```