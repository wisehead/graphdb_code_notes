#1.RawNode::on_persist_ready

```
RawNode::on_persist_ready
--let (mut index, mut term) = (0, 0);
--let mut snap_index = 0;
--while let Some(record) = self.records.front() {
----if record.number > number {
                break;
            }
----let record = self.records.pop_front().unwrap();

----if let Some((i, _)) = record.snapshot {
                snap_index = i;
                index = 0;
                term = 0;
            }

----if let Some((i, t)) = record.last_entry {
                index = i;
                term = t;
            }
--}
--if snap_index != 0 {
            self.raft.on_persist_snap(snap_index);
        }
--if index != 0 {
            self.raft.on_persist_entries(index, term);
        }

```