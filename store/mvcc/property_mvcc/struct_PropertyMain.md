#1.struct PropertyMain

```rust
pub struct PropertyMain {
    pub value: HashMap<FieldId, Value>,
    // currently TransactionId = TransactionTs
    pub commit_ts: TransactionTs,
    pub is_committed: Option<Arc<AtomicBool>>,
    pub is_deleted: bool,

    // chain to delta list
    // the first Arc to make PropertyMain be clonable so that read method don't need to lock the entire method which may properly block write
    // RwLock to make sure delta list change is thread safe
    // second Arc to make PropertyUndoDelta clonable so that it can be linked and owned by transaction
    pub deltas: Arc<RwLock<Option<Arc<PropertyUndoDelta>>>>,
}
```