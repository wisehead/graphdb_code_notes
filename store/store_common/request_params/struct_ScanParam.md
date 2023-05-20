#1.struct ScanParam

```rust
#[derive(Clone, Debug, Default)]
pub struct ScanParam {
    pub partition_id: PartitionId,
    pub type_id: GraphObjectTypeId,
    pub condition: Condition,
}
```