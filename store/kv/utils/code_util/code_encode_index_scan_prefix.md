#1.encode_index_scan_prefix

```
encode_index_scan_prefix
--let (content_code, indicator_code) = encode_index_binary(properties)?;
--let bin_content_len = content_code.len();
--let bin_indicators_len = indicator_code.len();

--let mut result = encode_index_prefix(graph_id, partition_id, key_type, index_id)?;
--result.reserve(bin_content_len + bin_indicators_len);

    // index binaries
--result.extend(content_code);
--result.extend(indicator_code);

```