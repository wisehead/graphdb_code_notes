#1.Partition::scan_completed

```
Partition::scan_completed
--let map = self.offset.borrow();

--for (_, v) in map.iter() {
            if !matches!(*v, Offset::End) {
                return false;
            }
        }

--true

```