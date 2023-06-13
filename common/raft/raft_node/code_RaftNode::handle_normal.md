#1.RaftNode::handle_normal

```
RaftNode::handle_normal
--let seq: u64 = deserialize(entry.get_context())?;
--match (
            deserialize::<Proposals>(entry.get_data())?,
            self.uncommitteds.remove(&seq),
----(Proposals::One(data), chan) => {
------let reply = self.store.apply(&data).await;
------if let Some(ReplyChan::One((chan, inst))) = chan {
--------let res = match reply {
                        Ok(data) => RaftResponse::Response { data },
                        Err(e) => RaftResponse::Error(e.to_string()),            
----(Proposals::More(mut datas), chans) => {
------let mut chans = if let Some(ReplyChan::More(chans)) = chans {
                    Some(chans)
------while let Some(data) = datas.pop() {
--------let reply = self.store.apply(&data).await;
--------if let Some((chan, inst)) = chans.as_mut().and_then(|cs| cs.pop()) {
----------let res = match reply {
                            Ok(data) => RaftResponse::Response { data },
                            Err(e) => RaftResponse::Error(e.to_string()),
```