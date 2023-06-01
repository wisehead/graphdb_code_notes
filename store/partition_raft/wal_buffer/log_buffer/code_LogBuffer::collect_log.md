#1.LogBuffer::collect_log

```
LogBuffer::collect_log
--let _lock = self.commit.lock().await;
--let capacity = Config::get_dml_log_capacity();
--let end_index = end_lsn as usize % capacity;
--if !self.logs[end_index].is_valid() {
----// It has already been committed by other thread
----return vec![];
--let sync_lsn_log = LogEntry::build(
            self.logs[end_index].lsn,
            self.logs[end_index].term,
            self.logs[end_index].txn_id,
            ActionTypeLog::SyncLSN,
            None,
        );
--let mut logs = vec![];
--if capacity == 1 {
            logs.push(self.logs[end_index].clone());
            self.logs[end_index] = LogEntry::default();
--} else {    
----for lsn in self.start_lsn..=end_lsn {
------let index = lsn as usize % capacity;
------while !self.logs[index].is_valid() {
--------self.notify.notified().await;
------logs.push(self.logs[index].clone());
------self.logs[index] = LogEntry::default(); 
--logs.push(sync_lsn_log);

--self.start_lsn = end_lsn + 1;
--self.notify.notify_waiters();  
```