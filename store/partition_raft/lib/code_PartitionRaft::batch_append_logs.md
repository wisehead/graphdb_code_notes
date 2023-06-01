#1.PartitionRaft::batch_append_logs

```
PartitionRaft::batch_append_logs
--if let Some(map) = MailboxMap::get()
            .inner
            .read()
            .await
            .get(&(graph_id, partition_id))
----if let Some(mailbox) = map.get(&peer_id) {
------// sync apppend log for raft sequence requirement
------for log in logs.iter() {
--------let message = serialize(&log).unwrap();
--------mailbox
                        .send(message)
                        .await
                        .map_err(|e| ErrorCode::RaftCommonError(e.to_string()))?;
```