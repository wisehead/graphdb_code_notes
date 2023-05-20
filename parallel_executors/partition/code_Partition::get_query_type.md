#1.Partition::get_query_type

```
Partition::get_query_type
--let map = self.offset.borrow();
--for (key, value) in map.iter() {
            if !matches!(*value, Offset::End) {
                return (*key, value.clone());
            }
        }
--(0, Offset::None)
```