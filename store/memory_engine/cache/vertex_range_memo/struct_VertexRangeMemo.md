#1.struct VertexRangeMemo

```rust
pub struct VertexRangeMemo {
    pub(super) memo: HashMap<VertexRangeKey, (VertexKey, VertexKey)>, /* type_id -> (min_val,
                                                                       * max_val) */
}
```