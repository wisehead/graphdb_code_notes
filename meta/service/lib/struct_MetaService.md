#1.struct MetaService

```rust
pub struct MetaService {
    pub(crate) tso: Box<dyn TimeStampOracle>,
    pub(crate) min_read_ts_manager: MinReadTsManager,
}

```