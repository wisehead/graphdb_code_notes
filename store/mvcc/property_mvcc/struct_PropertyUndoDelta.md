#1.struct PropertyUndoDelta

```rust
pub struct PropertyUndoDelta {
    pub old_val: HashMap<FieldId, Value>,

    pub prev: RwLock<Arc<PropertyPrevNodeWrapper>>, // the prev will either be main or delta, so don't need Option here
    pub next: RwLock<Option<Arc<PropertyUndoDelta>>>,
    // currently TransactionId = TransactionTs
    pub commit_ts: RwLock<TransactionTs>,
    pub op_type: OperationType,
}
```