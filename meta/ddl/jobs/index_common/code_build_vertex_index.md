#1.build_vertex_index

```
build_vertex_index
--let executor = create_vertex_scan_executor(graph_id, type_id);
--while !executor.scan_completed() {
----let result = executor
            .scan_vertex(stmt_ctx.clone(), &ScanParam::default())
            .await?;
```