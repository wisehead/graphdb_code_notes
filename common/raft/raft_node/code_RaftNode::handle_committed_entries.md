#1.RaftNode::handle_committed_entries

```
RaftNode::handle_committed_entries
--for entry in committed_entries {
----if entry.data.is_empty() {
      // From new elected leaders.
------continue;
----if let EntryType::EntryConfChange = entry.get_entry_type() {
------self.handle_config_change(&entry).await?;
----} else {
------self.handle_normal(&entry).await?;
--}
```