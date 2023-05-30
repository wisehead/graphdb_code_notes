#1.RaftServer::new

```
RaftServer::new
--let addr = addr.to_socket_addrs().unwrap().next().unwrap();
--RaftServer { addr, timeout }

```

#2.caller

```
async_main
--start_partition_raft_server//6001
--raft_engine::init//5001
```