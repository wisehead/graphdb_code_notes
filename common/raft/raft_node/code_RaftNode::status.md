#1.RaftNode::status

```
RaftNode::status
--let leader_id = self.raft.leader_id;
--Status {
            id: self.inner.raft.id,
            leader_id,
            uncommitteds: self.uncommitteds.len(),
            active_mailbox_sends: active_mailbox_sends(),
            active_mailbox_querys: active_mailbox_querys(),
            active_send_proposal_grpc_requests: send_proposal_active_requests(),
            active_send_message_grpc_requests: send_message_active_requests(),
            peers: self.peer_addrs(),
            term: self.inner.raft.term,
            current_lsn: 0, // self.store().get_current_lsn(),
            min_lsn: 0,     //self.store().get_min_lsn(),
            promotable: self.raft.promotable(),
        }

```