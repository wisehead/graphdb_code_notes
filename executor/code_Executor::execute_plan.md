#1.Executor::execute_plan

```
Executor::execute_plan
--let cache = SessionManager::get_instance().get_local_query_cache();
--

```

#2.caller

```
Executor::execute
--Executor::execute_plan
```

#3.caller of Executor::execute

```
- GrpcQueryService::query
// common/proto/query.proto
```