#1.encode_index_prefix

```
encode_index_prefix
--encode_header_with_key_type
--offset += K_SIZE_HEADER;
--NumberCodec::encode_u32_le(
        &mut result[offset..offset + K_SIZE_GRAPH_OBJECT_TYPE_ID],
        index_id,
    );
```