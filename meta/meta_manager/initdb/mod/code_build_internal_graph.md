#1.build_internal_graph

```
build_internal_graph
--let graph = Graph {
        id: systemdb_constants::SYSTEM_GRAPH_ID,
        name: String::from(systemdb_constants::SYSTEM_GRAPH_NAME),
        comment: String::from(systemdb_constants::SYSTEM_GRAPH_COMMENT),
        partition_number: systemdb_constants::SYSTEM_GRAPH_PARTITION_NUM,
        create_time: if let Ok(t) = SystemTime::now().duration_since(SystemTime::UNIX_EPOCH) {
            t.as_secs()
        } else {
            0
        },
        replica_number: systemdb_constants::SYSTEM_GRAPH_REPLICATION_NUM,
        ..Graph::default()
    };
```