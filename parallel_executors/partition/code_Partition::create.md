#1.Partition::create

```
Partition::create
--let offset: HashMap<GraphObjectTypeId, Offset> =
            vertex_type_id.iter().map(|x| (*x, Offset::None)).collect();
--Self {
            partition_id,
            scan_limit: RefCell::new(scan_limit),
            offset: RefCell::new(offset),
            cached_data: RefCell::default(),
            cached_row_num: RefCell::new(0),
        }

```