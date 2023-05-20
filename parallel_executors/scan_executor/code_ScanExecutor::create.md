#1.	ScanExecutor::create

```
ScanExecutor::create
-- if let Ok(p) = MetaClient::get().get_local_partitions(graph_id) {
            let num = p.len() as u32;
            let mut scan_limit: u32 = Config::get(None).computing.batch_scan_size;
            if num > 0 {
                scan_limit /= num;
            }
            for iter in p.iter() {
                partitions.push(Arc::new(Partition::create(//create partition
                    *iter,//partition_id
                    scan_limit,
                    type_ids.clone(),
                )));
            }
        }

--Self {
            graph_id,
            partitions,
        }
```