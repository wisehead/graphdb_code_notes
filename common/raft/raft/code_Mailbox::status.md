#1.Mailbox::status

```
Mailbox::status
--let (tx, rx) = oneshot::channel();
--let mut sender = self.sender.clone();
--let result = sender.send(Message::Status { chan: tx }).await;
--match result {
----Ok(_) => {
------let received_result = timeout(self.grpc_timeout, rx).await;
------match received_result {
                    Ok(Ok(RaftResponse::Status(status))) => Ok(status),
                    Ok(Ok(RaftResponse::Error(e))) => Err(Error::from(e)),
                    _ => Err(Error::Unknown),
```