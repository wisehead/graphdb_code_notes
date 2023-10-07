#1.MetaManager::register_node

```
MetaManager::register_node
--let cluster_info = if let Some(cluster) = self.clusters.get(&cluster_id) {
            cluster.clone()
--} else {
            // The first node of current cluster
            let cluster = Arc::new(ClusterInfo::init(cluster_id).await?);
            self.clusters.insert(cluster_id, cluster.clone());
            new_cluster = true;

            cluster
--};
```