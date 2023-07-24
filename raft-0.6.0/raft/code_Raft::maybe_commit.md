#1.Raft::maybe_commit

```
Raft::maybe_commit
--let mci = self.mut_prs().maximal_committed_index().0;
--if self.r.raft_log.maybe_commit(mci, self.r.term) {
            let (self_id, committed) = (self.id, self.raft_log.committed);
            self.mut_prs()
                .get_mut(self_id)
                .unwrap()
                .update_committed(committed);
            return true;
        }
        false
```