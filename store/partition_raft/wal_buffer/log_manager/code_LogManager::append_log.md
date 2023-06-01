#1.LogManager::append_log

```
LogManager::append_log
--let key = format!("{}-{}", graph_id, partition_id);
--let buffer_map = self.buffer_map.read().unwrap();
--let buffer_entry = buffer_map.get(&key);
--match buffer_entry {
----Some(m) => {
------let buffer = m.clone().load(Ordering::SeqCst);
------StorageExecutor::instance().spawn(unsafe { (*buffer).append_log(entry) });
```