#1.ScanExecutor::update_scan_limit

```
ScanExecutor::update_scan_limit
--let count = self
            .partitions
            .iter()
            .filter(|x| !x.scan_completed())
            .count();
--if count > 0 && count != self.partitions.len() {
            // update scan limit
----let scan_limit = Config::get(None).computing.batch_scan_size as u32 / count as u32;
----self.partitions
                .iter()
                .for_each(|x| x.update_scan_limit(scan_limit));
        }
```