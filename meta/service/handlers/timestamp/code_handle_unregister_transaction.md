#1.handle_unregister_transaction

```
handle_unregister_transaction
--let ts: Vec<TransactionTs> = batch_ts
        .batch_ts
        .into_iter()
        .map(|ts_msg| ts_msg.ts.into())
        .collect();
--let ts = MetaService::get()
        .min_read_ts_manager
        .unregister(&ts)
        .await?;
--Ok(tonic::Response::new(ReplyMsg {
        status: (ReplyStatus::KOk as i32),
        msg: String::new(),
        data: vec![transform_ts_to_value_msg(ts)],
    }))
```