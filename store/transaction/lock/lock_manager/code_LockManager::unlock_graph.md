#1.LockManager::unlock_graph

```
unlock_graph
--let mut graph_lock_map = self.graph_lock_map.lock().await;
--if let Some(lock_request_queue) = graph_lock_map.get_mut(&graph_id) {
----if lock_request_queue
                .remove_lock_by_transaction(txn_id)
                .is_ok()
------lock_request_queue.get_notify().notify_waiters();
------if lock_request_queue.is_empty() {
--------graph_lock_map.remove(&graph_id);
```