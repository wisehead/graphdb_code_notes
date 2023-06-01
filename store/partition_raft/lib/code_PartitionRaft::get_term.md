#1.PartitionRaft::get_term

```
PartitionRaft::get_term
--if let Some(map) = MailboxMap::get()
            .inner
            .read()
            .await
            .get(&(graph_id, partition_id)) &&
            let Some(peer_id) = MetaClient::get()
                .get_partition_peer_id(graph_id, partition_id) &&
            let Some(mailbox) = map.get(&(peer_id as u64))
        {
----let response = mailbox.status().await.unwrap();
----return Ok(response.term);
```