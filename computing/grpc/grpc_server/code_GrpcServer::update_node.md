#1.GrpcServer::update_node

```
GrpcServer:: update_node
--let msg = request.get_ref();
--let delete = msg.delete;
--let node: Node = util::deserialize_object(&msg.node)?;
--MetaHelper::get().upsert_node(node, delete);
```