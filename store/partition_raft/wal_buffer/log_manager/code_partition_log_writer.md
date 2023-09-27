#1.partition_log_writer

```
partition_log_writer
--loop {
    // Timeouted wait
----log_buffer.user_flush_timeout_wait().await;


  // Miscellaneous check put here
--if let Err(error) = log_buffer.check_error() {
            arcgraph_log::store_error!(
                "[PartitionLogManager] graph {} partition {} has error, error code is {:?}",
                log_buffer.graph_id,
                log_buffer.partition_id,
                error
            );

            // We loop for ever until aborted by PartitionLogManager through leader transfer
            continue;
        }

    // collect contiguous writable LogEntry's LSNs from log buffer
----let opt_write_interval = log_buffer.collect_log();
        if opt_write_interval.is_none() {
            // Nothing to do
            continue;
        }
----let (write_start_lsn, write_end_lsn) = opt_write_interval.unwrap();

        // Write log to temporary Vec according to collected LSN interval
        //
        // make room for append log as soon as possible
        // maybe OOM risk
        //

----let logs = log_buffer
            .write_log(write_start_lsn, write_end_lsn)
            .unwrap();
        // Flush log to RAFT
        //
        // need handle error from RAFT
        //

----if let Err(error) = log_buffer.flush_log(logs).await {
            // when error(leader change or disk full), we should set
            // error code to notify user task to report error
            // TODO: consider recover from error, such as disk full
------log_buffer.set_error(error);
------log_buffer.wakeup_user_flush();

            // We should loop and report error, not quit
            continue;
        }
        // Notify user flush wait
        //

        log_buffer.notify_log();
--}//end loop
```