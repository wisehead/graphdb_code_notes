#1.encode_vertex_index

```
encode_vertex_index
--let mut result = encode_index_scan_prefix(
        key.graph_id,
        key.partition_id,
        KeyType::VERTEX_NON_UNIQUE_INDEX,
        index_id,
        properties,
    )
    .unwrap();
--result.extend(key.encode_id());
```