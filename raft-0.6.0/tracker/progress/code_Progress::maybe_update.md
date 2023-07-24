#1.Progress::maybe_update

```
    /// Returns false if the given n index comes from an outdated message.
    /// Otherwise it updates the progress and returns true.
Progress::maybe_update
--let need_update = self.matched < n;
        if need_update {
            self.matched = n;
            self.resume();
        };

        if self.next_idx < n + 1 {
            self.next_idx = n + 1
        }

        need_update
```