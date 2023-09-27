#1.LogBuffer::flush_log

```
LogBuffer::flush_log
--let flush_lsn = logs.last().unwrap().lsn;
--PartitionRaft::get()
            .batch_append_logs(self.graph_id, self.partition_id, self.peer_id, logs)
            .await?;
--self.set_flush_lsn(flush_lsn);            
```