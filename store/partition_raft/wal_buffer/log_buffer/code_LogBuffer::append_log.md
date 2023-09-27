#1.LogBuffer::append_log

```
LogBuffer::append_log
--let current_lsn = log.lsn;
--let index = current_lsn as usize % self.config.log_buffer_size;

--while (current_lsn - self.get_write_lsn()) as usize >= self.config.log_buffer_size {
            // The buffer is already full
            // wait log writer to make room
            self.sleep_and_check().await?;
--}

--// When log writer call write_log, Vec's splice method will shorten logs length for a while,
--// append_log can be called during this phase, so we skip length check to avoid access panic
--unsafe {
            *self.logs.as_mut_slice().get_unchecked_mut(index) = log;
        }

--while !self.links.has_space(current_lsn) {
            // The link buffer is already full
            // wait log writer to make room
            self.sleep_and_check().await?;
--}
--self.links.add_link_advance_tail(current_lsn, current_lsn + 1);
```