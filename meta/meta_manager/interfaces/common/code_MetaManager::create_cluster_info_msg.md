#1.MetaManager::create_cluster_info_msg

```
MetaManager::create_cluster_info_msg
--let cluster = match self.clusters.get(&cluster_id)
--let meta_node = self.get_meta_leader()?;
--let meta_leader = util::serialize_object(&meta_node).unwrap();

--let nodes: Vec<_> = cluster
            .nodes
            .iter()
            .map(|n| util::serialize_object(n.value()).unwrap())
            .collect();
--let graphs: Vec<_> = cluster
            .graphs
            .iter()
            .map(|g| GraphInfoMsg::from(g.value().clone().as_ref()))
            .collect();
--Ok(ClusterInfoMsg {
            meta_leader,
            nodes,
            graphs,
        })
```