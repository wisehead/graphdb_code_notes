#1.PartitionLogManager::new

```
PartitionLogManager::new
--let init_lsn = Self::get_init_lsn();
--let log_buffer = LogBuffer::build(graph_id, partition_id, init_lsn, config);
--let log_buffer_ptr = Box::into_raw(Box::new(log_buffer));

  // TODO: maybe need a std::thread for performance
--let log_writer_handle = PartitionRaftExecutor::instance()
            .spawn(unsafe { partition_log_writer(log_buffer_ptr.as_mut().unwrap()) });
--Self {
            graph_id,
            partition_id,
            current_lsn: AtomicU64::new(init_lsn),
            log_buffer: AtomicPtr::new(log_buffer_ptr),
            log_task_handles: vec![log_writer_handle],
        }
```