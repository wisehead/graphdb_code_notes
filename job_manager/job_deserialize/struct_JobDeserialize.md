#1.struct JobDeserialize

```rust
pub struct JobDeserialize {
    // Deserialize callback for each derived Job struct
    deserialize_fn: RwLock<HashMap<JobType, Box<JobDeserializeFn>>>,
}
pub type JobDeserializeFn = fn(&str, TransactionTs) -> Result<Arc<dyn Job>>;
```