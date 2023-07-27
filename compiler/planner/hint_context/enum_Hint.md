#1.enum Hint

```rust
/// Hint used for controlling plan generation
#[derive(PartialEq, Eq, PartialOrd, Ord, Debug, Clone)]
pub enum Hint {
    DistTempResult,
    IgnorePlanCache,
    MatThruFilter,
    NoMatThruFilter,
    MatThruSort,
    NoMatThruSort,
    UseEdgeScan,
    NoUseEdgeScan,
    UseIndexScan,
    NoUseIndexScan,
}
```