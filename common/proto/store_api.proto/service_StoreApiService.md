#1.service StoreApiService

```proto
service StoreApiService {
  rpc HandleRemoteQueryRequest(QueryRequest) returns (ReplyMsg) {}
}
```