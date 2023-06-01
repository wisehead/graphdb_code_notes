#1.Transaction::write_commit_log

```
Transaction::write_commit_log
--for part_id in self.modified_partitions.iter() {
----self.append_log(ActionTypeLog::CommitTxn, *part_id, None)
                .await?;
```