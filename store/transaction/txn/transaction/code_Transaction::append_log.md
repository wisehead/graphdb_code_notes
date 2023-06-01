#1.Transaction::append_log
```
Transaction::append_log
--let log_instance = LogManager::instance();
--let lsn = log_instance.get_lsn(self.graph_id, part_id);
--let term = PartitionRaft::get()
            .get_term(self.graph_id, part_id)
            .await?;
--let log_entry = LogEntry::build(lsn, term as i64, self.txn_id, action_type, graph_log);
--LogManager::instance().append_log(self.graph_id, part_id, log_entry)
```