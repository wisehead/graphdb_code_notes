#1.struct ScanExecutor

```rust
#[derive(Debug)]
pub struct ScanExecutor {
    graph_id: GraphId,
    partitions: Vec<Arc<Partition>>,
}

```