#1.convert_to_log_entries

```
convert_to_log_entries
--if entry.entry_type == EntryType::EntryNormal && !entry.get_data().is_empty() {
----if let Ok(proposals) = bincode::deserialize::<Proposals>(entry.get_data()) {
------match proposals {
--------Proposals::More(logs) => {
----------for log_data in logs.iter() {
------------if let Ok(log_entry) = bincode::deserialize::<LogEntry>(log_data) {
--------------result.push(log_entry);
--------Proposals::One(log_data) => {
----------if let Ok(log_entry) = bincode::deserialize::<LogEntry>(&log_data) {
----------result.push(log_entry);

```