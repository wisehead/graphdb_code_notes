#1.Raft::request_leader

```
Raft::request_leader
--let (leader_id, leader_addr): (u64, String) = {
----let mut client = RaftServiceClient::connect(format!("http://{}", peer_addr)).await?;
----let response = client
                .request_id(Request::new(Empty {
                    graph_id: cluster.0,
                    partition_id: cluster.1,
                }))
                .await?
                .into_inner();
----match response.code() {
------ResultCode::WrongLeader => {
                    let (leader_id, addr): (u64, Option<String>) = deserialize(&response.data)?;
                    if let Some(addr) = addr {
                        (leader_id, addr)
                    } else {
                        return Ok(None);
                    }
                }
------ResultCode::Ok => (deserialize(&response.data)?, peer_addr),
------ResultCode::Error => return Ok(None),
```

#2.caller

```
- Raft::find_leader_info
- Raft::join
```