#1.Partition::handle_query_result

```
Partition::handle_query_result
--let row_num = data.rows.len();
--if self.get_cached_row_num() == 0 {
----*self.cached_data.borrow_mut() = data;
--} else {
            self.cached_data
                .borrow_mut()
                .deref_mut()
                .rows
                .append(&mut data.rows);
        }

--*self.cached_row_num.borrow_mut() += row_num as u32;
--self.set_offset(type_id, offset);
```

#2.caller

```
Partiton::scan
```