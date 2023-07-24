#1.RaftLog::maybe_persist

```
RaftLog::maybe_persist
--let first_update_index = match &self.unstable.snapshot {
            Some(s) => s.get_metadata().index,
            None => self.unstable.offset,
        };
--if index > self.persisted
            && index < first_update_index
            && self.store.term(index).map_or(false, |t| t == term)
        {
            debug!(self.unstable.logger, "persisted index {}", index);
            self.persisted = index;
            true
--} else {
            false
        }
```