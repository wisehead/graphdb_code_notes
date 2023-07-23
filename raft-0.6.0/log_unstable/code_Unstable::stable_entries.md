#1.Unstable::stable_entries

```
Unstable::stable_entries
--if let Some(entry) = self.entries.last() {
            if entry.get_index() != index || entry.get_term() != term {
                fatal!(
                    self.logger,
                    "the last one of unstable.slice has different index {} and term {}, expect {} {}",
                    entry.get_index(),
                    entry.get_term(),
                    index,
                    term
                );
            }
            self.offset = entry.get_index() + 1;
            self.entries.clear();
            self.entries_size = 0;
        }
```