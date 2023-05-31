#1.SledStorage::get_entries

```
SledStorage::get_entries
--let real_high = if let Some(size) = max_size.into() {
            if size < high - low {
                low + size + 1
            } else {
                high
            }
        } else {
            high
        };
--let start: &[u8] = &low.to_le_bytes();
--let end: &[u8] = &real_high.to_le_bytes();
--let r = self.core.range(start..end);
--let mut entries = vec![];
--for bytes_entry in r {
----let bytes = bytes_entry?;
            // entries.push(Entry::parse_from_bytes(&bytes.1).unwrap());
----if let Ok(entry) = Entry::parse_from_bytes(&bytes.1) {
------entries.push(entry);        
```