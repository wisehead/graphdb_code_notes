#1.BuildIndexJob::build_index

```
BuildIndexJob::build_index
--let type_id_set: HashSet<GraphObjectTypeId> =
            self.index_info.iter().map(|x| x.type_id).collect();
--let graph_id = self.get_graph_id();
--let mut task_vec = vec![];
--let type_id_vec: Vec<GraphObjectTypeId> = type_id_set.iter().cloned().collect();            
--let handler = Concurrency::spawn(async move {
----//lambda
----if is_vertex {
------build_vertex_index(ctx, graph_id, id, info).await
----} else {
------build_edge_index(ctx, graph_id, id, info).await
----});//end of lambda
--task_vec.push(handler);
```