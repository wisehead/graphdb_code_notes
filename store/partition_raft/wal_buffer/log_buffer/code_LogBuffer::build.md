#1.LogBuffer::build

```
LogBuffer::build
--let mut peer_id = 0;
--if cfg!(not(feature = "test-mock")) {
            let peer = MetaHelper::get().get_partition_peer_id(graph_id, partition_id);
            if peer.is_none() {
                panic!(
                    "[PartitionLogManager] Not found peer id when build log buffer for graph {} partition {}",
                    graph_id, partition_id
                );
            }
            peer_id = peer.unwrap();
        }

--let logs = vec![LogEntry::default(); config.log_buffer_size];

--let links = Box::new(LinkBuffer::new(config.log_recent_written_size));
--links.add_link(0, init_lsn);
--links.advance_tail();

--Self {
            graph_id,
            partition_id,
            peer_id,
            config,
            write_lsn: AtomicU64::new(init_lsn),
            flush_lsn: AtomicU64::new(init_lsn),
            notify_lsn: AtomicU64::new(init_lsn),
            logs,
            links,
            user_task_notify: Notify::new(),
            log_writer_notify: Notify::new(),
            log_has_error: AtomicBool::new(false),
            log_error_code: None,
        }

```