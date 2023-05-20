#1.ScanExecutor::scan_completed

```
ScanExecutor::scan_completed
--if self.partitions.is_empty() {
            true
--} else {//make sure all the partitions are done.
            self.partitions
                .iter()
                .all(|partition| partition.scan_completed())
        }
```