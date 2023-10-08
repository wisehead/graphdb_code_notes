#1.GraphMetaData::init_with_graph

```
GraphMetaData::init_with_graph
--let partitions = Self::fetch_partitions(cluster_id, id, meta_store.clone()).await?;
--let partition_peer_info =
            Self::fetch_partition_info(cluster_id, id, meta_store.clone()).await?;
--let partitions = Self::fetch_partitions(cluster_id, id, meta_store.clone()).await?;

        let partition_peer_info =
            Self::fetch_partition_info(cluster_id, id, meta_store.clone()).await?;

        let (e_schemas, e_names) = Self::fetch_edge_types(cluster_id, id, meta_store.clone())
            .await
            .with_context(|| {
                ErrorCode::InitializeError(format!(
                    "Fail to initialize edge type cache for graph id: {}",
                    id
                ))
            })?;
        let (v_schemas, v_names) = Self::fetch_vertex_types(cluster_id, id, meta_store.clone())
            .await
            .with_context(|| {
                ErrorCode::InitializeError(format!(
                    "Fail to initialize vertex type cache for graph id: {}",
                    id
                ))
            })?;
        let (i_schemas, i_names) = Self::fetch_indices(cluster_id, id, meta_store.clone())
            .await
            .with_context(|| {
                ErrorCode::InitializeError(format!(
                    "Fail to initialize index type cache for graph id: {}",
                    id
                ))
            })?;

        Ok(Self {
            graph: RwLock::new(graph),
            partition_id_leader_map: RwLock::new(partitions),
            partition_peer_info: RwLock::new(partition_peer_info),
            edge_schemas: Arc::new(RwLock::new(e_schemas)),
            vertex_schemas: Arc::new(RwLock::new(v_schemas)),
            index: Arc::new(RwLock::new(i_schemas)),
            edge_type_name_map: Arc::new(e_names),
            vertex_type_name_map: Arc::new(v_names),
            index_name_map: Arc::new(i_names),
        })            
```