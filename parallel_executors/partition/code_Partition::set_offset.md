#1.Partition::set_offset

```
Partition::set_offset
--let mut map = self.offset.borrow_mut();
--map.entry(id)
            .and_modify(|e| *e = offset.clone())
            .or_insert(offset);
```

#2.caller

```
handle_query_result
```