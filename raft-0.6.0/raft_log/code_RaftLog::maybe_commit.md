#1.RaftLog::maybe_commit

```
RaftLog::maybe_commit
--if max_index > self.committed && self.term(max_index).map_or(false, |t| t == term) {
            debug!(
                self.unstable.logger,
                "committing index {index}",
                index = max_index
            );
            self.commit_to(max_index);
            true
        } else {
            false
        }
```