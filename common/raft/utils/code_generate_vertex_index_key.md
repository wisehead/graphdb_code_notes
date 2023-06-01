#1.generate_vertex_index_key

```
generate_vertex_index_key
--let indexes = meta_client.get_indexes_by_schema_id(graph_id, vertex_key.type_id);
--if properties.is_some() {
        for index in indexes.iter() {
            for property in properties.unwrap().iter() {
                if index.use_property_id(&property.id) {
                    related_indexes.push(index.clone());
                }
            }
        }
--} else {
        related_indexes = indexes;
--for index in related_indexes.iter() {
----let mut index_used_values = vec![];
----for field in index.get_field_ids() {
------if let Some(value) = m.get(&field) {
--------index_used_values.push(value.clone());
----let index_key = encode_vertex_index(index.id, index_used_values, vertex_key);
----result.push(index_key.unwrap());
```