#1.Raft::on_persist_entries

```
Raft::on_persist_entries
--let update = self.raft_log.maybe_persist(index, term);
--if update && self.state == StateRole::Leader {
```