#1.LogBuffer::commit_log

```
LogBuffer::commit_log
--let meta = MetaClient::get();
--let peer_id = meta.get_partition_peer_id(graph_id, partition_id).unwrap();
--PartitionRaft::get()
            .batch_append_logs(graph_id, partition_id, peer_id as u64, logs)
            .await
```