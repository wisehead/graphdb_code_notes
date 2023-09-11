#1.MinReadTsManager::unregister

```
MinReadTsManager::unregister
--for ts in batch {
----let remove_item = self.active_ts.remove(ts);
----if remove_item.is_none() {
------meta_warn!("The ts {:?} is not existed in MinReadTsManager", ts);
--let min_read_ts = {
    // if there's still active transaction, use the min ts for the active transaction
----if let Some(min_ts) = self.active_ts.front() {
------(*min_ts).clone()
----} else {
      // if there's no active transaction, use the removed (last transaction ts + 1)
------let last_ts = batch.iter().max().ok_or_else(|| {
                    ErrorCode::UpdateMinReadTsError(
                        "Cannot unregister with empty batch of ts.".to_string(),
                    )
                })?;
------TransactionTs::from(last_ts.get_num() + 1)
----}
--};
--self.persist(&min_read_ts).await.with_context(|| {
            // rollback mem updates
            batch.iter().for_each(|ts| {
                self.active_ts.insert(ts.clone());
            });
            ErrorCode::UpdateMinReadTsError("Fail to persist min read ts.".to_string())
--})?;
```