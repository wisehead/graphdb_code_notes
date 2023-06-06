#1.RenameGraphProcessor::prepare

```
RenameGraphProcessor::prepare
--self.lock(stmt_ctx).await?;
--let meta = MetaClient::get();
--let _ = meta.update_graph_name_by_id(
            self.op.from_id.unwrap(),
            &self.op.from_name,
            &self.op.to_name,
        )?;
--set_node_info()
```