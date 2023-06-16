#1.struct LogGuard

```rust

pub struct LogGuard {
    pub log_guard: WorkerGuard,
    //emm... will be fix in tracing_subscriber v0.4
    pub reload_handle: Option<
        reload::Handle<
            EnvFilter,
            Layered<
                Option<
                    Filtered<
                        Layer<Registry, DefaultFields, Format, NonBlocking>,
                        tracing_subscriber::reload::Layer<EnvFilter, Registry>,
                        Registry,
                    >,
                >,
                Registry,
            >,
        >,
    >,
    pub audit_log_guard: WorkerGuard,
    pub audit_reload_handle: Option<reload::Handle<EnvFilter, Registry>>,
}
```