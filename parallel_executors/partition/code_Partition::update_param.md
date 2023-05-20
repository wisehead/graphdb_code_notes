#1.Partition::update_param

```
Partition::update_param
--let (type_id, offset) = self.get_query_type();
--match param {
----ExecutorParam::Edge(edge_param) => {
                let mut object = edge_param.clone();
                object.partition_id = self.partition_id;
                object.type_id = type_id;
                object.condition.update(
                    Limit::Limit(*self.scan_limit.borrow() - self.get_cached_row_num()),
                    offset,
                );
                ExecutorParam::Edge(object)
            }
----ExecutorParam::Index(index_param) => {
                let mut object = index_param.clone();
                object.partition_id = self.partition_id;
                object.condition.update(
                    Limit::Limit(*self.scan_limit.borrow() - self.get_cached_row_num()),
                    offset,
                );
                ExecutorParam::Index(object)
            }
----ExecutorParam::Vertex(vertex_param) => {
                let mut object = vertex_param.clone();
                object.partition_id = self.partition_id;
                object.type_id = type_id;
                object.condition.update(
                    Limit::Limit(*self.scan_limit.borrow() - self.get_cached_row_num()),
                    offset,
                );
                ExecutorParam::Vertex(object)
            }
        }
```