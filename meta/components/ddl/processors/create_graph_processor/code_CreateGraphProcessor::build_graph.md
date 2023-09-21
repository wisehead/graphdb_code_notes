#1.CreateGraphProcessor::build_graph

```
CreateGraphProcessor::build_graph
--let id = self.inner.op.graph_id.unwrap();

        let name = self.inner.op.graph_name.clone();
        let comment = match &self.inner.op.comment {
            Some(c) => c.clone(),
            None => String::new(),
        };
        let partition_number = self.inner.op.partition_number;
        let create_time = if let Ok(t) = SystemTime::now().duration_since(SystemTime::UNIX_EPOCH) {
            t.as_secs()
        } else {
            0
        };

        let replica_number = self.inner.op.replica_number.unwrap();

        let graph = Graph {
            id,
            name,
            comment,
            partition_number,
            create_time,
            replica_number,
            ..Graph::default()
        };

        Ok(graph)
```