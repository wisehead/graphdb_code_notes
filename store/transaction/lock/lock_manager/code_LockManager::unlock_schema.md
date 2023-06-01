#1.LockManager::unlock_schema

```
LockManager::unlock_schema
--let mut schema_lock_map = self.schema_lock_map.lock().await;
--if let Some(lock_request_queue) = schema_lock_map.get_mut(&schema_id) {
```