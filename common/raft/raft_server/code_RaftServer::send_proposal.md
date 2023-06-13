#1.RaftServer::send_proposal

```
RaftServer::send_proposal
--//这个sender是raft状态机的sender，创建状态机的时候保存在mailbox。
--let mut sender = MailboxMap::get()
            .inner
            .read()
            .await
            .get(&cluster)
            .unwrap()
            .get(&peer_id)
            .unwrap()
            .sender
            .clone();
--let (tx, rx) = oneshot::channel();
--let message = Message::Propose { proposal, chan: tx };
--let reply = match sender.try_send(message) {
----Ok(()) => match timeout(self.timeout, rx).await {
------Ok(Ok(raft_response)) => match serialize(&raft_response) {
--------Ok(resp) => Ok(Response::new(raft_service::RaftResponse { inner: resp })),
```