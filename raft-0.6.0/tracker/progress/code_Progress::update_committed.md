#1.Progress::update_committed

```
 /// update committed_index. of Progress project
Progress::update_committed
--if committed_index > self.committed_index {
            self.committed_index = committed_index
        }
```