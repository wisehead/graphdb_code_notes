#1.encode_value

```
encode_value
--let mut result = Vec::with_capacity(4 + null_size + values.len() * 8);
--result.extend_from_slice(schema_version.to_le_bytes().as_ref());
--let mut fixed_buffer: Vec<u8> = Vec::new();
--let mut non_fixed_buffer: Vec<&[u8]> = Vec::new();
--let mut non_fixed_offset = 0i32;
--for (index, value) in values.iter().enumerate() {
----match value {
------Value::None => {
                if let Some(null_index) = null_index_map.get(&index) {
                    null_indicator[*null_index] = true;
                }
            }
------Value::String(data) | Value::Text(data) => {
                non_fixed_buffer.push(data.as_bytes());
                let data_len = data.len() as i32;
                // offset
                fixed_buffer.extend_from_slice(non_fixed_offset.to_le_bytes().as_ref());
                // length
                fixed_buffer.extend_from_slice(data_len.to_le_bytes().as_ref());
                non_fixed_offset += data_len;
            }
------Value::Blob(data) => {
                let inline_blob_val = data.as_inline_blob().unwrap().value();
                non_fixed_buffer.push(inline_blob_val);
                let data_len = inline_blob_val.len() as i32;
                fixed_buffer.extend_from_slice(non_fixed_offset.to_le_bytes().as_ref());
                // length
                fixed_buffer.extend_from_slice(data_len.to_le_bytes().as_ref());
                non_fixed_offset += data_len;
            }
------_ => {
                if let Some(encode) = value.encode() {
                    fixed_buffer.extend(encode);
                }
            }
----}
        
```