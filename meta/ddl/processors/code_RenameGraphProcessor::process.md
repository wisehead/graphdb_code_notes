#1.RenameGraphProcessor::process

```
RenameGraphProcessor::process
--let tso = MetaClient::get().get_transaction_ts(false).await?.get_num();
--let new_stmt_ctx = StmtCtx {
            txn_id: tso,
            stmt_tso: tso,
            ..stmt_ctx.clone()
        };
--let request = self.create_request(DdlStep::KStepPrepare, &new_stmt_ctx)?;
--self.handle_request(request, &new_stmt_ctx).await?;
--self.build_response_msg(false)        
```