#1.LogBuffer::append_log

```
LogBuffer::append_log
--let capacity = Config::get_dml_log_capacity();
--let current_lsn = log.lsn;
--let commit_flag = log.action_type.is_finish_action();
--let index = current_lsn as usize % capacity;
--let mut diff = current_lsn - self.start_lsn;
--while diff >= capacity as u64 {
----// The buffer is already full
----self.notify.notified().await;
----diff = current_lsn - self.start_lsn;
----self.logs[index] = log;
----self.notify.notify_waiters();
----if commit_flag || self.is_full(current_lsn) {
------let logs = self.collect_log(current_lsn).await;
------if !logs.is_empty() {
--------let graph_id = self.graph_id;
--------let partition_id = self.partition_id;
--------if matches!(Config::get_dml_log_policy(), LogPolicy::Performance) {
----------StorageExecutor::instance().spawn(Self::commit_log(
                        graph_id,
                        partition_id,
                        logs,
                    ));
--------} else {
----------return Self::commit_log(graph_id, partition_id, logs).await;
```