#1.TransactionWrapper::query_vertex

```
TransactionWrapper::query_vertex
--let txn_inner = self.txn.read().await;
--let inserted_vertices = txn_inner.modifies.get_upserted_vertices();
--let ret1 = inserted_vertices
            .into_iter()
            .filter(|key| key.type_id == type_id && key.partition_id == partition_id)
            .map(|v| {
                (
                    v.clone(),
                    txn_inner.modifies.get_vertex_prop_values(&v).unwrap(),
                )
            })
            .collect();

--let removed_vertices = txn_inner.modifies.get_removed_vertices();
--let ret2 = removed_vertices
            .into_iter()
            .filter(|key| key.type_id == type_id && key.partition_id == partition_id)
            .collect();
```