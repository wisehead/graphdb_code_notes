#1.RaftNode::on_ready

```
RaftNode::on_ready
--let mut ready = self.ready();
--if !ready.messages().is_empty() {
    // Send out the messages.
----let messages = ready.take_messages();
----self.send_messages(messages);
```