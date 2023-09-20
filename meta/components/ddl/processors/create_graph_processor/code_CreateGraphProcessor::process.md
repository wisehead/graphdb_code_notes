#1.CreateGraphProcessor::process

```
CreateGraphProcessor::process
--if !is_meta_leader() {
----let request = self.create_request(DdlStep::KStepForward, stmt_ctx)?;
----return self.forward(request).await;
--let cluster_id = stmt_ctx.cluster_id;
--let meta_mgr = MetaManager::get();
--let cluster = MetaManager::get().get_cluster(cluster_id)?;
--if cluster
            .get_graph_id_by_name(&self.inner.op.graph_name)
            .is_ok()
        {
            return if self.inner.op.if_check_existence {
                self.build_response_msg(true)
            } else {
                Err(ErrorCode::GraphAlreadyExistsError(format!(
                    "Graph name is {}",
                    self.inner.op.graph_name
                )))
            };
        }
--let request = self
            .update_and_create_request(&meta_mgr, &cluster, stmt_ctx)
            .await?;
----prepare
--self.handle_request(request, stmt_ctx).await?;
--self.build_response_msg(false)
```