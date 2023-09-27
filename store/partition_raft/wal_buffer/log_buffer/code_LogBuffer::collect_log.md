#1.LogBuffer::collect_log

```
LogBuffer::collect_log
--let write_start_lsn = self.get_write_lsn();
--let write_max_size = self.config.log_write_max_size;
--let stop_func =
            |prev_lsn: u64, _next_lsn: u64| (prev_lsn - write_start_lsn) as usize > write_max_size;
        self.links.advance_tail_until(&stop_func, 0);
        let write_end_lsn = self.get_ready_for_write_lsn();
--if write_start_lsn == write_end_lsn {
----None
--} else {
----Some((write_start_lsn, write_end_lsn))
        }
```