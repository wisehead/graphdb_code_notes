#1.recovery

```
recovery
--if refresh_cache && memory_engine::MemoryEngine::is_global_topology_cache_enabled() 
----let instances = GraphInstances::get();
----instances
            .recovery_partition_data(graph_id, partition_id)
            .await
            .unwrap();
--// 2. replay log, flush data into tikv and edge topology into memengine
--let mut txn_set: HashSet<TransactionId> = HashSet::new();
--let mut commit_logs: Vec<LogEntry> = Vec::new();
--let mut assist_map: HashMap<TransactionId, Vec<LogEntry>> = HashMap::new();
--let mut commit_txns: Vec<TransactionTs> = Vec::new();
--for entry in logs.iter() {
----let log_entries = convert_to_log_entries(entry);
----if config::Config::is_enable_transaction() {
------for log_entry in log_entries.iter() {
--------match log_entry.action_type {
----------ActionTypeLog::StartTxn => {
                        assist_map.entry(log_entry.txn_id).or_insert(Vec::new());
                    }
----------ActionTypeLog::CommitTxn => {
                        txn_set.remove(&log_entry.txn_id);
                        if let Some(index_data) = assist_map.get(&log_entry.txn_id) {
                            commit_logs.extend_from_slice(index_data);
                            commit_txns.push(log_entry.txn_id.into());
                            assist_map.remove(&log_entry.txn_id);
                        }
                    }
----------ActionTypeLog::RollbackTxn => {
                        commit_txns.push(log_entry.txn_id.into());
                        txn_set.remove(&log_entry.txn_id);
                    }
----------_ => {
                        if let Some(data) = assist_map.get_mut(&log_entry.txn_id) {
                            data.push(log_entry.clone());
                        }
                    }
                }
----else {
------for log_entry in log_entries.iter() {
--------commit_logs.push(log_entry.clone());  
--// 3. Sort index to bring back the index with previous order  and then replay these logs
--commit_logs.sort_by(|a, b| a.lsn.cmp(&b.lsn));
--let mut kv_map: HashMap<Key, Value> = HashMap::new();
--let mut update_vertex_map: HashMap<Key, Vec<data_type::Value>> = HashMap::new();
--let mut update_edge_map: HashMap<Key, Vec<data_type::Value>> = HashMap::new();
--let mut delete_keys: Vec<Key> = Vec::new();

--let mut insert_edge_keys: Vec<EdgeKey> = vec![];
--let mut delete_edge_keys: Vec<EdgeKey> = vec![];              
--for log_entry in commit_logs.iter() {
----match log_entry.action_type {
------ActionTypeLog::InsertVertex => {
--------if let Some(log_data) = &log_entry.action_log {
----------if let GraphObjectKey::Vertex(key) = &log_data.key {
------------if let GraphObjectProperty::Insert(values) = &log_data.property {
------------// Encode value
------------let schema = meta_client
               .get_vertex_schema_by_id(graph_id, key.type_id)
               .unwrap();
------------let encode_value = encode_value(
--------------log_data.schema_version,
--------------values,
--------------&schema.generate_null_index_map(),
------------kv_map.insert(key.encode(), encode_value);
------------let mut m = HashMap::new();
------------for (idx, value) in values.iter().enumerate() {
--------------let field_id = schema.fields[idx].id;
--------------m.insert(field_id, value.clone());
------------// index
------------let index_keys = generate_vertex_index_key(graph_id, key, &m, None);
------------for index_key in index_keys.into_iter() {
--------------kv_map.insert(index_key, EMPTY_VALUE.into());


------ActionTypeLog::UpdateVertex => {
--------let schema = meta_client
                                .get_vertex_schema_by_id(graph_id, key.type_id)
                                .unwrap();
--------let filed_index_map = schema.generate_field_id_index_map();
--------let encode_key = key.encode();
--------// 判断是否已经缓存values数据
                            if update_vertex_map.get(&encode_key).is_none() {
                                if let Some(current_data) =
                                    kv_client.get(encode_key.clone()).await.unwrap()
                                {
                                    let decode_result = decode_properties(
                                        &current_data[..],
                                        &schema,
                                        &schema.field_names[..],
                                    );
                                    if decode_result.is_ok() {
                                        update_vertex_map
                                            .insert(encode_key.clone(), decode_result.unwrap());
                                    }
                                }
--------}
--------// 拿出来后根据变更属性重新更新values数据，如果多次进行更新操作，则会重复修改数据，再编码，这里可以做些优化，暂时先不处理
                            let mut old_value_map = HashMap::new();
                            let mut new_value_map = HashMap::new();
--------if let Some(values) = update_vertex_map.get_mut(&encode_key) {
----------for (idx, field) in schema.fields.iter().enumerate() {
------------old_value_map.insert(field.id, values[idx].clone());
----------for property in properties.iter() {
------------if let Some(index) = filed_index_map.get(&property.id) {
                                        old_values.push(Property {
                                            id: property.id,
                                            value: values[*index].clone(),
                                        });
                                        values[*index] = property.value.clone();
------------}
----------}
----------// build old index keys that need to be removed
----------let delete_index_keys = generate_vertex_index_key(
                                    graph_id,
                                    key,
                                    &old_value_map,
                                    Some(&old_values),
                                );
----------for index_key in delete_index_keys.into_iter() {
------------delete_keys.push(index_key);                                
----------// build new value map
----------for (idx, field) in schema.fields.iter().enumerate() {
                                    new_value_map.insert(field.id, values[idx].clone());
----------}

----------// build new index keys that need to be inserted
----------let index_keys = generate_vertex_index_key(
                                    graph_id,
                                    key,
                                    &new_value_map,
                                    Some(properties),
                                );
----------for index_key in index_keys.into_iter() {
                                    kv_map.insert(index_key, EMPTY_VALUE.into());
                                }

----------// 重新编码后放入kv_map
----------let encode_value = encode_value(
                                    log_data.schema_version,
                                    values,
                                    &schema.generate_null_index_map(),
                                );
----------kv_map.insert(encode_key, encode_value);
```