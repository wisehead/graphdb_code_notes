#1.Transaction::append_log
```
Transaction::append_log
--let log_instance = LogManager::instance();
--let lsn = log_instance.get_lsn(self.graph_id, part_id);
```