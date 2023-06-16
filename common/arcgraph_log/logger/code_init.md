#1.init

```
init
--let subscriber = Registry::default();
--global::set_text_map_propagator(TraceContextPropagator::new());
--let audit_file_appender =
        tracing_appender::rolling::daily(&config.audit_file_path, &config.audit_file_name);
--let (audit_file_writer, audit_guard) = tracing_appender::non_blocking(audit_file_appender);
--let (audit_file_layer, audit_reload_handle) = if config.enable_audit_file {
----let audit_filter = EnvFilter::new(&config.audit_env);
----let (audit_filter, audit_reload_handle) = reload::Layer::new(audit_filter);
----(
------Some(
                fmt::Layer::default()
                    .with_line_number(true)
                    .with_file(true)
                    .with_span_events(FmtSpan::NEW | FmtSpan::CLOSE)
                    .with_writer(audit_file_writer)
                    .with_ansi(false)
                    .with_filter(audit_filter),
            ),
------Some(audit_reload_handle),
----)
--let subscriber = subscriber.with(audit_file_layer);
--let file_appender = tracing_appender::rolling::hourly(&config.file_path, &config.file_name);
--let (file_writer, guard) = tracing_appender::non_blocking(file_appender);
--let (file_layer, reload_handle) = if config.enable_file {
----let env_filter = EnvFilter::new(&config.env);
----let (env_filter, reload_handle) = reload::Layer::new(env_filter);
----(
            Some(
                fmt::Layer::default()
                    .with_line_number(true)
                    .with_file(true)
                    .with_writer(file_writer)
                    .with_ansi(false)
                    .with_thread_ids(true)
                    .with_thread_names(true)
                    .with_filter(env_filter),
            ),
            Some(reload_handle),
----)
--let subscriber = subscriber.with(file_layer);

--let console_layer = if config.enable_console {
----let env_filter = EnvFilter::new(&config.env);
----Some(
            // tracing_logfmt::builder().with_span_name(false)
            //                          .with_span_path(false)
            //                          .with_target(true)
            //                          .layer()
            //                          .with_writer(std::io::stdout)
            //                          .with_filter(env_filter),
            fmt::Layer::default()
                .with_line_number(true)
                .with_file(true)
                .with_thread_ids(true)
                .with_thread_names(true)
                .with_writer(std::io::stdout)
                .with_filter(env_filter)
        )
--let subscriber = subscriber.with(console_layer);

--let opentelemetry = if config.enable_trace_report {
----let sampler = Sampler::TraceIdRatioBased(config.sample_ratio);
----let trace_config = opentelemetry::sdk::trace::config().with_resource(
                opentelemetry::sdk::Resource::new(vec![
                    opentelemetry::KeyValue::new("service.name", "arcg"),
                    opentelemetry::KeyValue::new("service.version", "0.1.0"),
                ]),
            ).with_sampler(sampler);

----let tracer = opentelemetry_otlp::new_pipeline()
            .tracing()
            .with_exporter(
                opentelemetry_otlp::new_exporter()
                    .tonic()
                    .with_endpoint(config.otel_endpoint.as_str()),
            )
            .with_trace_config(trace_config)
            .with_batch_config(BatchConfig::default().with_max_queue_size(16384))
            .install_batch(opentelemetry::runtime::Tokio)
            .unwrap();
----let opentelemetry = tracing_opentelemetry::layer().with_tracer(tracer);
----Some(opentelemetry)        
--let subscriber = subscriber.with(opentelemetry);

--tracing::subscriber::set_global_default(subscriber).expect("unable to set global subscriber");
--LogGuard {
        log_guard: guard,
        reload_handle,
        audit_log_guard: audit_guard,
        audit_reload_handle,
    }
```