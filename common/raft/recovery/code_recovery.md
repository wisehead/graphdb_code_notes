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
--              
```