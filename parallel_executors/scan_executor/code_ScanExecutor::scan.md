#1.ScanExecutor::scan

```
ScanExecutor::scan
--if self.partitions.is_empty() {
----return Result::Ok(vec![]);
--self.update_scan_limit();
--for p in self.partitions.iter() {
----if p.scan_completed() {
------continue;
----let new_param = param.clone();
----let partition = p.clone();

----let ctx = ctx.clone();
            let task =
                Concurrency::spawn(async move { partition.scan(ctx, new_param).await });

            task_vec.push(task);
--let result = future::join_all(task_vec).await;//
--for (index, iter) in result.into_iter().enumerate() {
----let inner_result = iter.unwrap();
----data_set.push(inner_result.unwrap());
--Result::Ok(data_set)
```