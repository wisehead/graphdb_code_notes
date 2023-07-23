#1.RawNode::commit_ready

```
RawNode::commit_ready
--if let Some(ss) = rd.ss {
            self.prev_ss = ss;
        }
--if let Some(hs) = rd.hs {
            self.prev_hs = hs;
        }
--let rd_record = self.records.back().unwrap();
--let raft = &mut self.raft;
--if let Some((index, _)) = rd_record.snapshot {
            raft.raft_log.stable_snap(index);
        }
--if let Some((index, term)) = rd_record.last_entry {
----raft.raft_log.stable_entries(index, term);
------RaftLog::stable_entries
--------Unstable::stable_entries
```