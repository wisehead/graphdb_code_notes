#1.LocalNotified::run

```
LocalNotified::run
--let raw = self.task.raw;
--mem::forget(self);
--raw.poll();

```