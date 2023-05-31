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
--let mut peer_node_map = HashMap::new();
--for (_, value) in partition_peers.iter() {
----for peer in value.iter() {
------peer_node_map.insert(peer.1 as u64, peer.0.clone());
--for (key, value) in partition_peers.iter() {
----let partition_id = key;
----if let Some(leader_id) = meta.get_partition_peer_id(graph_id, partition_id.to_owned()) {
------current_leader_id = leader_id;
----for (node, peer_id) in value.iter() {
------if host_id != node.id {
--------continue;
------let raft_addr = format!("{}:{}", node.ip, partition_raft_port);
------let store = HashStore::new(graph_id, partition_id.to_owned(), *peer_id as u64);
------let cluster = (graph_id, partition_id.to_owned());
------// graph_id: u32, partition_id: u32, peer_id: i64, log_folder: Option<String>
------let storage = SledStorage::new(graph_id, *partition_id, *peer_id, None);
------// let storage = MemStorage::create();
------let raft = Raft::new(
          graph_id,
          *partition_id as u32,
          node.id,
          raft_addr,
          store,
          logger.clone(),
          cfg.clone(),
          storage,
          cluster,
          true,
      );
------mailbox_map
                .inner
                .write()
                .await
                .entry(cluster)
                .or_insert_with(HashMap::new);

------mailbox_map
                .inner
                .write()
                .await
                .get_mut(&cluster)
                .unwrap()
                .insert(*peer_id as u64, Arc::new(raft.mailbox()));
------if current_leader_id == *peer_id {
--------tokio::spawn(raft.lead(*peer_id as u64, cluster));
------else
--------if let Some(leader_node) = peer_node_map.get(&(current_leader_id as u64)){
                    leader_addr = format!("{}:{}", leader_node.ip, partition_raft_port);
--------}else if let Some(peer) = meta.fetch_peer_status(graph_id, *partition_id, current_leader_id as u64).await{
                    let node = meta.get_node_by_id(peer.node_id).unwrap();
                    leader_addr = format!("{}:{}", node.ip, partition_raft_port);
--------}
--------tokio::spawn(raft.join(
                    *peer_id as u64,
                    Some(current_leader_id as u64),
                    leader_addr,
                    cluster,
                    false,
                ));
                
```

#2.caller

```
init_raft
```