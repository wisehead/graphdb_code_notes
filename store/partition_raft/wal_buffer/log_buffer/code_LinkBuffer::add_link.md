#1.LinkBuffer::add_link

```
LinkBuffer::add_link
--let index = self.slot_index(start_lsn);
--self.link_buffer[index].store(end_lsn, Ordering::Release);
```