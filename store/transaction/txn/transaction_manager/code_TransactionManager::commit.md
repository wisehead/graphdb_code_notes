#1.TransactionManager::commit

```
TransactionManager::commit
--if let Some(wrapper) = self.txn_map.read().await.get(&txn_id) {
----let mut txn = wrapper.txn.write().await;
----if txn.get_txn_type() == TransactionType::ReadWrite {
                txn.write_commit_log().await?;
----txn.set_commit_ts(commit_ts);
----txn.set_txn_state(TransactionState::Commit);
----txn.release_lock().await;                
```