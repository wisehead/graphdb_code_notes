#1.MetaClient::update_graph_name_by_id

```
MetaClient::update_graph_name_by_id
--let meta_cache = self.get_graph_meta_cache(graph_id)?;
--meta_cache.update_graph_name(new_name.to_owned());
--self.cache
            .update_graph_name_id_map(graph_id, old_name, new_name)?;

```