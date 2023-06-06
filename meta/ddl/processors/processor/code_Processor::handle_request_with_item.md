#1.Processor::handle_request_with_item

```
Processor::handle_request_with_item
--GraphActionManager::instance().add_graph_item(graph_item.clone())?;
--let result = self.dispatch_prepare(request).await;
--let result = self.commit(stmt_ctx).await;
--GraphActionManager::instance().remove_graph_item(graph_item);
```