#1.IdSource::fetch_next_batch_ids

```
IdSource::fetch_next_batch_ids
--let key = self.prefix.as_str();
--let result = self.meta_store.txn_get(key, false).await?;
--let result = self.meta_store.txn_get(key, false).await?;
--let value_str = {
            if let Some(first_element) = result.get(0) {
                first_element.value_str()?.to_string()
            } else {
                let value_str = if key.contains(K_CURRENT_GRAPH_ID_PREFIX) {
                    GRAPH_ID_INIT_NUM.to_string()
                } else {
                    "0".to_string()
                };
                meta_info!("Initialize id source for key: {}, val: {}", key, value_str);
                let mut temp_map: HashMap<String, String> = HashMap::new();
                temp_map.insert(key.to_string(), value_str.to_string());
                self.meta_store.txn_put(&temp_map).await?;
                value_str
            }
        };
--let start = value_str.to_string().parse::<u64>()
--let end = start + size;
--let mut temp_map: HashMap<String, String> = HashMap::new();
--temp_map.insert(key.to_string(), end.to_string());
--let resp = self.meta_store.txn_put(&temp_map).await;
```