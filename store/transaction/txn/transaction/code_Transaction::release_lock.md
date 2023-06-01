#1.Transaction::release_lock

```
Transaction::release_lock
--if let Some(graph_id) = self.acquired_locks.get_graph() {
----for schema_id in self.acquired_locks.get_schemas() {
------LockManager::get()
                    .unlock_schema(self.txn_id, *schema_id)
                    .await;
----LockManager::get().unlock_graph(self.txn_id, graph_id).await;
--self.acquired_locks.clear()
```