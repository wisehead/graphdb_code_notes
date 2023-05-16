#1.VertexScanExecutor::scan_vertex

```
VertexScanExecutor::scan_vertex
--for p in self.partitions.iter() {
----let new_param = param.clone();
----let partition = p.clone();
----let ctx = ctx.clone();
----let task = Concurrency::spawn(async move { partition.scan_vertex(ctx, new_param).await });
----task_vec.push(task);
```