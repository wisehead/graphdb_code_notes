#1.SledStorage::new

```
SledStorage::new
--file_path = format!("/tmp/raft_log/sled/{graph_id}_{partition_id}_{peer_id}")
--Self {
            graph_id,
            partition_id,
            core: sled::open(file_path).unwrap(),
            active_txns: RefCell::default(),
            snapshot_metadata: SnapshotMetadata::default(),
        }

```

#2.caller 

```
- init_graph_partition_raft
```