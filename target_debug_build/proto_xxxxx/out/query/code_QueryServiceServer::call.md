#1.QueryServiceServer::call

```
QueryServiceServer::call
--"/query.QueryService/Query" => 
----QuerySvc::call
------(*inner).query(request).await
----let res = grpc.unary(method, req).await;
```