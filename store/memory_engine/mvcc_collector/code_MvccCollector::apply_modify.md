#1.MvccCollector::apply_modify

```
MvccCollector::apply_modify
--match modify {
----Modify::InsertVertex(vertex, _) => {
------self.apply_insert_vertex_for_topology(&vertex.vid);
------self.apply_vertex_modify(&vertex.vid, modify, start_ts).await
```