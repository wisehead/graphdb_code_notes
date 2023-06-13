#1.struct Entry

```rust
#[derive(PartialEq,Clone,Default)]
pub struct Entry {
    // message fields
    pub entry_type: EntryType,
    pub term: u64,
    pub index: u64,
    pub data: ::bytes::Bytes,
    pub context: ::bytes::Bytes,
    pub sync_log: bool,
    // special fields
    pub unknown_fields: ::protobuf::UnknownFields,
    pub cached_size: ::protobuf::CachedSize,
}

```