#1.enum Task

```rust
pub enum Task {
    Cpu(CpuTaskHandle),
    Network(NetworkTaskHandle),
}

```