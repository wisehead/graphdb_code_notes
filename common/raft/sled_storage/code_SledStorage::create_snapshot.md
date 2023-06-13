#1.SledStorage::create_snapshot

```
SledStorage::create_snapshot
--self.snapshot(0).map_err(|e| Error::Other(Box::new(e)))
```

#2.SledStorage::snapshot

```
snapshot
--let mut snapshot = Snapshot::default();
--let meta = snapshot.mut_metadata();

--let hard_state = self.get_hard_state()
--meta.index = hard_state.get_commit();
--meta.term = if meta.index == self.snapshot_metadata.get_index() {
----self.snapshot_metadata.get_term()
--} else {
----let entry = self
                .get_entry(meta.index)
                .map_err(|e| self.build_tikv_error(e))?
                .unwrap_or_else(|| panic!("entry with {} should exists", meta.index));
----entry.term
--let conf_state = self
            .get_conf_state()
--meta.set_conf_state(conf_state);
--if snapshot.get_metadata().index < request_index {
----snapshot.mut_metadata().index = request_index;            
--Ok(snapshot)
```