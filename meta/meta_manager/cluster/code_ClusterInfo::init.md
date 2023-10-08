#1.ClusterInfo::init

```
ClusterInfo::init
--let tso = meta_tso::timestamp_oracle::Tso::new(cluster_id)
--let meta_store = meta_store::MetaStore::get_instance();
--let nodes = GraphMetaData::fetch_nodes(cluster_id, meta_store.clone())
--let (graphs, graph_names) = Self::init_graphs(cluster_id, meta_store.clone()).await?;
--let config_data =
            Self::init_arcserver_config_data(cluster_id, &nodes, meta_store.clone()).await?;
--let graph_id_pool = IdPool::new(IdSource {
            prefix: format_meta_key!(cluster_id, K_CURRENT_GRAPH_ID_PREFIX),
            meta_store: meta_store.clone(),
        })?;
--let job_id_pool = IdPool::new(IdSource {
            prefix: format_meta_key!(cluster_id, K_CURRENT_JOB_ID_PREFIX),
            meta_store: meta_store.clone(),
        })?;

--let min_read_ts_manager = MinReadTsManager::new(cluster_id).await;
--let cluster = Self {
            cluster_id,
            nodes,
            graphs,
            graph_names,
            graph_id_pool,
            job_id_pool,
            graph_object_id_pools: DashMap::new(),
            field_id_pools: DashMap::new(),
            tso,
            min_read_ts_manager,
            meta_store: meta_store.clone(),
            config_data,
        };
--cluster
            .init_graph_id_pools(meta_store.clone())
            .await
            .expect("Fail to init graph id-pools.");
--Ok(cluster)
```