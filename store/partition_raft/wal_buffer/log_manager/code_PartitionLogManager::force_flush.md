#1.PartitionLogManager::force_flush

```
PartitionLogManager::force_flush
--let waiting_lsn = self.get_current_lsn() - 1;
--self.get_log_buffer()
            .wait_flush_log(waiting_lsn, true)
            .await?;
```