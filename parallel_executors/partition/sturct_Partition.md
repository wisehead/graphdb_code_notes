#1.struct Partition

```rust
#[derive(Debug, Clone)]
pub struct Partition {
    pub(crate) partition_id: PartitionId,
    scan_limit: RefCell<u32>,
    offset: RefCell<HashMap<GraphObjectTypeId, Offset>>,
    cached_data: RefCell<DataSet>,
    cached_row_num: RefCell<u32>,
}

```