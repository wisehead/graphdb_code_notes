#1.PartitionLogManager::commit_flush

```
PartitionLogManager::commit_flush
--self.get_log_buffer()
            .wait_flush_log(commit_lsn, false)
            .await?;
```