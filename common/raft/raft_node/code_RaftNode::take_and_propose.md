#1.RaftNode::take_and_propose

```
RaftNode::take_and_propose
--if let Some((data, reply_chans)) = merger.take() {
----let seq = self.seq.fetch_add(1, Ordering::Relaxed);
----self.uncommitteds.insert(seq, reply_chans);
----let seq = serialize(&seq).unwrap();
----let data = serialize(&data).unwrap();
----self.propose(seq, data)
------RawNode::propose
```