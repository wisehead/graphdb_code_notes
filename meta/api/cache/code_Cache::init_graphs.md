#1.Cache::init_graphs

```
Cache::init_graphs
--let response = fetch_key_value(
            client.clone(),
            K_GRAPH_PREFIX,
            Some(GetOptions::new().with_prefix()),
        )
        .await?;

```