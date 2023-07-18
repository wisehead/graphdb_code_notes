#1.HashStore::query

```
HashStore::query
--let query: Message = deserialize(query).unwrap();
--let data: Vec<u8> = match query {
----Message::Get { key } => {
------if let Some(val) = self.get(&key) {
--------HashStore::get
----------self.data.read().unwrap().get(key).cloned()
--------serialize(&val).unwrap()
------} else {
--------Vec::new()
----_ => Vec::new(),
```

#2.caller: RaftNode::send_query

```rust
async fn send_query(&self, query: &[u8], chan: oneshot::Sender<RaftResponse>) {
        let data = self.store.query(query).await.unwrap_or_default();
        if let Err(e) = chan.send(RaftResponse::Response { data }) {
            warn!("Message::Query, RaftResponse send error: {:?}", e);
        }
    }
```

#3.RaftNode::run

```rust
Ok(Some(Message::Query { query, chan })) => {
                    let now = Instant::now();
                    if !self.is_leader() {
                        debug!("[forward_query] query.len: {:?}", query.len());
                        self.forward_query(query, chan).await;
                    } else {
                        debug!("Message::Query, {:?}", query);
                        self.send_query(&query, chan).await;
                    }
                    if now.elapsed() > self.cfg.heartbeat {
                        info!("Message::Query elapsed: {:?}", now.elapsed());
                    }
                }

```