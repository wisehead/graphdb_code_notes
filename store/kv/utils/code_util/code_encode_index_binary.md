#1.encode_index_binary

```
encode_index_binary
--for property in properties {
----match property {
            Value::Boolean(v) => {
                let mut bin: Vec<u8> = vec![0; K_SIZE_BOOL];
                content_len += K_SIZE_BOOL;
                NumberCodec::encode_u8(&mut bin[0..], v.into());
                contents.push(bin);
            }
            Value::Int32(v) => {
                let mut bin: Vec<u8> = vec![0; K_SIZE_INT_32];
                content_len += K_SIZE_INT_32;
                NumberCodec::encode_u32(&mut bin[0..], encode_i32_to_comparable_u32(v));
                contents.push(bin);
            }
            Value::Int64(v) => {
                let mut bin: Vec<u8> = vec![0; K_SIZE_INT_64];
                content_len += K_SIZE_INT_64;
                NumberCodec::encode_u64(&mut bin[0..], encode_i64_to_comparable_u64(v));
                contents.push(bin);
            }
            Value::Float(v) => {
                let mut bin: Vec<u8> = vec![0; K_SIZE_FLOAT];
                content_len += K_SIZE_FLOAT;
                NumberCodec::encode_u32(&mut bin[0..], encode_f32_to_comparable_u32(v));
                contents.push(bin);
            }
            Value::Double(v) => {
                let mut bin: Vec<u8> = vec![0; K_SIZE_DOUBLE];
                content_len += K_SIZE_DOUBLE;
                NumberCodec::encode_u64(&mut bin[0..], encode_f64_to_comparable_u64(v));
                contents.push(bin);
            }
            Value::Timestamp(v) => {
                let mut bin: Vec<u8> = vec![0; K_SIZE_UINT_64];
                content_len += K_SIZE_UINT_64;
                NumberCodec::encode_u64(&mut bin[0..], v);
                contents.push(bin);
            }
            Value::String(v) => {
                let size = v.len();
                content_len += size;
                len_indicators.push(size as u32);
                contents.push(v.into());
            }
            other => {
                store_error!("Value type not supported to be encoded into index binary");
                return Err(ErrorCode::UnsupportedIndexValueType(format!("{:?}", other)));
            }
        }
--}
--let mut content = Vec::with_capacity(content_len);
--contents.into_iter().for_each(|v| {
        content.extend(v);
    });
--let mut indicator_count = len_indicators.len();
--let mut indicator_code = vec![0; indicator_count * 4];
--let mut offset = 0;
--while indicator_count != 0 {
----indicator_count -= 1;
----NumberCodec::encode_u32(
            &mut indicator_code[offset..],
            // ^ SIGN_MARK_32 should be removed when data import logic is fixed
            // length is unsigned and should not do comparable number convert
            len_indicators[indicator_count] ^ SIGN_MARK_32,
        );
        offset += K_SIZE_UINT_32;
--}
    
```