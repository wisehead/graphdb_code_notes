#1.Partition::scan

```
Partition::scan
--while !self.scan_completed() {
----let new_param = self.update_param(&param);
----let type_id = new_param.get_type_id();
----let (data, offset) = match new_param {
------ExecutorParam::Vertex(scan_param) => {
                    store_api::scan_vertex(scan_param, ctx.clone()).await?
                }
------ExecutorParam::Edge(scan_param) => {
                    store_api::scan_edge(scan_param, ctx.clone()).await?
                }
------ExecutorParam::Index(scan_param) => {
                    store_api::scan_vertex_index(scan_param, ctx.clone()).await?
                }
            };
----self.handle_query_result(data, offset, type_id);
----if flag {
------return self.produce_result();
            }
```