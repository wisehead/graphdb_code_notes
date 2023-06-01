#1.LockManager::unlock_schema

```
LockManager::unlock_schema
--let mut schema_lock_map = self.schema_lock_map.lock().await;
--if let Some(lock_request_queue) = schema_lock_map.get_mut(&schema_id) {
----if lock_request_queue
                .remove_lock_by_transaction(txn_id)
                .is_ok()
------lock_request_queue.get_notify().notify_waiters();
------if lock_request_queue.is_empty() {
--------schema_lock_map.remove(&schema_id);                
```