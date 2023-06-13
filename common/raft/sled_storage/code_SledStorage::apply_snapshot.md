#1.SledStorage::apply_snapshot

```
SledStorage::apply_snapshot
--let meta = snapshot.get_metadata();
--let first_index = self.get_first_index()
--self.snapshot_metadata = meta.clone();
--let r = self.get_hard_state()?;
--let mut hard_state = if let Some(hs) = r {
----hs
--hard_state.term = cmp::max(meta.term, hard_state.term);
--hard_state.commit = cmp::max(meta.index, hard_state.commit);
--let conf_state = meta.get_conf_state();
--let last_index = self.get_last_index()
--self.core.transaction(|tx| {
----let mut del_batch = Batch::default();
----for key in first_index..=last_index {
                del_batch.remove(&key.to_be_bytes());
            }

----tx.apply_batch(&del_batch)?;

----tx.insert(&FIRST_INDEX, &(meta.index + 1).to_be_bytes())?;
----tx.insert(&LAST_INDEX, &meta.index.to_be_bytes())?;

----tx.insert(
                &HARD_STATE,
                hard_state
                    .write_to_bytes()
                    .expect("hard state should be able to bytes"),
            )?;

----tx.insert(
                &CONF_STATE,
                conf_state
                    .write_to_bytes()
                    .expect("conf state should be able to bytes"),
            )?;
----Ok(())
--})?;
--self.active_txns.borrow_mut().clear();
```