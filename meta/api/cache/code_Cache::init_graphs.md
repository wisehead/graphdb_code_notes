#1.Cache::init_graphs

```
Cache::init_graphs
--let response = fetch_key_value(
            client.clone(),
            K_GRAPH_PREFIX,//所有的图id"/fabarta/graph/"
            Some(GetOptions::new().with_prefix()),
        )
        .await?;
--for kv in response.kvs() {
            let value_str = kv.value_str();
            if value_str.is_err() {
                continue;
            }
            let graph = Graph::from(value_str.unwrap());
            if graph.status == SchemaStatus::Deleted {
                continue;
            }
            let id = graph.id;
            graph_names.insert(graph.name.clone(), id);

            let data = GraphMetaCache::init_with_graph(client.clone(), graph).await?;
            meta_debug!("Initiated graph [{}].", id);
            graph_data.insert(id, Arc::new(data));
        }

```

#2.caller

- Cache::init