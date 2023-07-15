#1.Raft::tick_heartbeat

```
Raft::tick_heartbeat
--self.heartbeat_elapsed += 1;
--self.election_elapsed += 1;

--if self.election_elapsed >= self.election_timeout {
----self.election_elapsed = 0;
----if self.check_quorum {
------let m = new_message(INVALID_ID, MessageType::MsgCheckQuorum, Some(self.id));
------has_ready = true;
------let _ = self.step(m);
----if self.state == StateRole::Leader && self.lead_transferee.is_some() {
------self.abort_leader_transfer()

--if self.state != StateRole::Leader {
----return has_ready;
--if self.heartbeat_elapsed >= self.heartbeat_timeout {
----self.heartbeat_elapsed = 0;
----has_ready = true;
----let m = new_message(INVALID_ID, MessageType::MsgBeat, Some(self.id));
----let _ = self.step(m);
--has_ready
```