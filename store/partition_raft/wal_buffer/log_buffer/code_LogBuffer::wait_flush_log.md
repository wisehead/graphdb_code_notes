#1.LogBuffer::wait_flush_log

```
LogBuffer::wait_flush_log
--self.wakeup_log_writer();
--if force || matches!(self.config.log_flush_policy, LogFlushPolicy::Security) {
            // Wait until waiting_lsn has been flushed
            while waiting_lsn >= self.get_flush_lsn() {
                self.user_flush_timeout_wait().await;
                self.check_error()?
            }
        }
```