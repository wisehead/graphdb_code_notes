#1.struct ConfChange

```rust
#[derive(PartialEq,Clone,Default)]
pub struct ConfChange {
    // message fields
    pub change_type: ConfChangeType,
    pub node_id: u64,
    pub context: ::bytes::Bytes,
    pub id: u64,
    // special fields
    pub unknown_fields: ::protobuf::UnknownFields,
    pub cached_size: ::protobuf::CachedSize,
}

```