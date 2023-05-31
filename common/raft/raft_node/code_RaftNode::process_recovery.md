#1.RaftNode::process_recovery

```
RaftNode::process_recovery
--if self.do_recovery && self.is_leader() {
----let storage = self.store();
------RawNode::store
--------self.raft.store()
----let first_index = storage.first_index().unwrap();
------SledStorage::first_index
--------SledStorage::get_first_index
----------let bytes_first_index = self.core.get(&FIRST_INDEX)?;//sled中
----let last_index = storage.last_index().unwrap();
----let logs = if last_index > first_index {
                storage.entries(
                        storage.first_index().unwrap(),
                        storage.last_index().unwrap(),
                        None,
                    )
                    .unwrap()
------SledStorage::entries
--------SledStorage::get_entries
```