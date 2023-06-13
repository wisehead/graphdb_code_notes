#1.ProposalSender::send

```
ProposalSender::send
--let result = self.client.send_proposal(self.proposal).await;
--match result {
----Ok(reply) => {
------let raft_response: RaftResponse = deserialize(&reply)?;
------Ok(raft_response)
```