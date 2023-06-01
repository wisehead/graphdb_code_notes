#1.LogManager::get_lsn

```
LogManager::get_lsn
--let key = format!("{}-{}", graph_id, partition_id);
----let lsn_map = self.lsn_map.read().unwrap();
----if let Some(lsn) = lsn_map.get(&key) {
------return lsn.fetch_add(1, Ordering::SeqCst);
--let mut lsn_map = self.lsn_map.write().unwrap();
--if !lsn_map.contains_key(&key) {
----let init_value = crate::get_init_lsn(graph_id, partition_id);
------let timestamp = SystemTime::now()
        .duration_since(UNIX_EPOCH)
        .unwrap()
        .as_secs() as u64;
------// 避免机器之间时间上的差异
------timestamp + 10000
----let mut buffer_map = self.buffer_map.write().unwrap();
----if buffer_map.get(&key).is_none() {
------let thread = std::thread::spawn(move || {
          StorageExecutor::instance().block_on(async move {
          let buffer =
             LogBuffer::build(graph_id, partition_id, init_value).await;
                                let buffer_ptr = Box::into_raw(Box::new(buffer));
                                Arc::new(AtomicPtr::new(buffer_ptr))
                            })
                        });
------if let Ok(v) = thread.join() {
--------buffer_map.insert(key.clone(), v);
----let entry = lsn_map
                    .entry(key)
                    .or_insert_with(|| AtomicU64::new(init_value));
----entry.fetch_add(1, Ordering::SeqCst)
--else {//f !lsn_map.contains_key(&key) {
----let lsn = lsn_map.get(&key).unwrap();
----lsn.fetch_add(1, Ordering::SeqCst)
```