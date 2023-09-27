#1.LogBuffer::sleep_and_check

```
LogBuffer::sleep_and_check
--self.wakeup_log_writer();

  // Should sleep very short, but not too short, pay attention to cpu cost
--tokio::time::sleep(Duration::from_micros(
            self.config.log_user_sleep_wait_ns as u64,
        ))
        .await;
--self.check_error()?;
```