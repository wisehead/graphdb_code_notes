#1.LogBuffer::write_log

```
LogBuffer::write_log
--let capacity = self.logs.capacity();
--let start_idx = write_start_lsn as usize % capacity;
--let end_idx = write_end_lsn as usize % capacity;
--let mut write_out_logs: Vec<LogEntry> = vec![];

        // Logs is a ring buffer, we want move, but not clone, LogEntry
        // between [start_idx, end_idx) or [start_idx, capacity) [0, end_idx)
        // from logs to write_out_logs, and we don't want logs's length be
        // changed when complete write out, so we use Vec's splice method to
        // drain writable LogEntry out and replace with default LogEntry
--if start_idx < end_idx {
            let replace_iter = std::iter::repeat(LogEntry::default()).take(end_idx - start_idx);
            let iter = self.logs.splice(start_idx..end_idx, replace_iter);
            for entry in iter {
                write_out_logs.push(entry);
            }
--} else {
            let replace_iter = std::iter::repeat(LogEntry::default()).take(capacity - start_idx);
            let iter = self.logs.splice(start_idx..capacity, replace_iter);
            for entry in iter {
                write_out_logs.push(entry);
            }
            let replace_iter = std::iter::repeat(LogEntry::default()).take(end_idx);
            let iter = self.logs.splice(0..end_idx, replace_iter);
            for entry in iter {
                write_out_logs.push(entry);
            }
        }

        if !write_out_logs.is_empty() {
            self.set_write_lsn(write_out_logs.last().unwrap().lsn);
        }

        Some(write_out_logs)
```