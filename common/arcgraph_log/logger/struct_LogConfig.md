#1.struct LogConfig

```rust

#[derive(Debug, Serialize, Deserialize)]
pub struct LogConfig {
    pub file_path: String,
    pub file_name: String,
    pub audit_file_path: String,
    pub audit_file_name: String,
    pub enable_console: bool,
    pub enable_file: bool,
    pub enable_audit_file: bool,
    pub env: String,
    pub audit_env: String,
    pub trace_level: String,
    pub otel_endpoint: String,
    #[serde(default)] // default is false
    pub enable_trace_report: bool,
    #[serde(default)] // default is 0.0
    pub sample_ratio: f64,
}

```