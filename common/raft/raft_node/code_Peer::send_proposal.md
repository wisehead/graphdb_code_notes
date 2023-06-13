#1.Peer::send_proposal

```
Peer::send_proposal
--let msg = RraftProposal {
            inner: msg,
            graph_id: self.cluster.0,
            partition_id: self.cluster.1,
            peer_id: self.peer_id,
        };
--let reply = self._send_proposal(msg).await;
--match reply {
            Ok(reply) => {
                self.record_success();
                Ok(reply)
            }        
```

#2.Peer::_send_proposal

```
Peer::_send_proposal
--let c = self.connect().await?;
--async fn task(mut c: RaftGrpcClient, msg: RraftProposal) -> Result<Vec<u8>> {
----let message_request = Request::new(msg);
----let response = c.send_proposal(message_request).await?;
------RaftServiceClient::send_proposal//发到RaftServiceServer:: send_proposal
----let message_reply = response.into_inner();
----Ok(message_reply.inner)
```