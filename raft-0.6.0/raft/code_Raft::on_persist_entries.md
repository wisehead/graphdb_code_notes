#1.Raft::on_persist_entries

```
Raft::on_persist_entries
--let update = self.raft_log.maybe_persist(index, term);
--if update && self.state == StateRole::Leader {
----// Actually, if it is a leader and persisted index is updated, this term
            // must be equal to self.term because the persisted index must be equal to
            // the last index of entries from previous leader when it becomes leader
            // (see the comments in become_leader), namely, the new persisted entries
            // must come from this leader.
----if term != self.term {
                error!(
                    self.logger,
                    "leader's persisted index changed but the term {} is not the same as {}",
                    term,
                    self.term
                );
            }
----let self_id = self.id;
----let pr = self.mut_prs().get_mut(self_id).unwrap();
----if pr.maybe_update(index) && self.maybe_commit() && self.should_bcast_commit() {
                self.bcast_append();
            }
```