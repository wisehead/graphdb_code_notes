#1.message QueryRequest

```proto
message QueryRequest {
  ActionType action_type = 1;
  bytes param = 2;
  bytes stmt_ctx = 3;
}
```