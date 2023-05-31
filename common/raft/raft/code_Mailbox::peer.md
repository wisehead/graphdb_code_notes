#1.Mailbox::peer

```
Mailbox::peer
--self.peers
            .entry((leader_id, leader_addr.clone()))
            .or_insert_with(|| {
                Peer::new(
                    leader_addr,
                    self.grpc_timeout,
                    self.grpc_concurrency_limit,
                    self.grpc_breaker_threshold,
                    self.grpc_breaker_retry_interval,
                    self.cluster,
                    leader_id,
                    host_id,
                    PeerRole::Voter,
                )
            })
            .clone()

```