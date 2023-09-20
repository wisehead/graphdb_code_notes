#1.Processor::handle_request_with_item

```
Processor::handle_request_with_item
--GraphActionManager::instance().add_graph_item(graph_item.clone())?;
--let result = self.dispatch_prepare(request, false, stmt_ctx).await;
--if result.is_err() {
            GraphActionManager::instance().remove_graph_item(graph_item.clone());
            result?;
        }
--let result = self.commit(stmt_ctx).await;
--GraphActionManager::instance().remove_graph_item(graph_item);
```