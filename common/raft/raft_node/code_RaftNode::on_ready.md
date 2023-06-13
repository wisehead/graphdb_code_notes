#1.RaftNode::on_ready

```
RaftNode::on_ready
--let mut ready = self.ready();
--if !ready.messages().is_empty() {
    // Send out the messages.
----let messages = ready.take_messages();
----self.send_messages(messages);

--if *ready.snapshot() != Snapshot::default() {
----let snapshot = ready.snapshot();
----self.store.restore(snapshot.get_data()).await?;
----let store = self.mut_store();
----store.apply_snapshot(snapshot.clone())?;
--}

--self.handle_committed_entries(ready.take_committed_entries())
            .await?;
```