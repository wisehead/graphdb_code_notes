#1.RaftServer::run

```
RaftServer::run
--let svc = RaftServiceServer::new(self);
--Server::builder()
            .add_service(svc)
            .serve(addr)
            .await
            .expect("error running server");
```