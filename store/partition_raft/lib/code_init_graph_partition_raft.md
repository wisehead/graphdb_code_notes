#1.init_graph_partition_raft

```
init_graph_partition_raft
--meta = MetaClient::get();
--let config = config::Config::get(None);
    let host_id = config.node.node_id as u64;
    let partition_raft_port = config::Config::get_partition_raft_port();//6001
    let cfg = Config::default();
--let logger = RaftLog::get().logger.clone();//raft专门的log库
----RaftLog::get
------RaftLog::new
--let mailbox_map = MailboxMap::get();
--let partition_peers = meta.get_graph_raft_info(graph_id);
```

#2.caller

```
init_raft
```