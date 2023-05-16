#1.Partition::scan_vertex

```
Partition::scan_vertex
--while !self.scan_completed() {
----let scan_param = self.update_vertex_param(&param);
----let type_id = scan_param.type_id;
----let (data, offset) = store_api::scan_vertex(scan_param, ctx.clone()).await?;
```