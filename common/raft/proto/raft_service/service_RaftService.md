#1.service RaftService

```proto

syntax = "proto3";
package raftservice;

//import "eraftpb.proto";

service RaftService {
  rpc RequestId(Empty) returns (IdRequestReponse) {}
  rpc ChangeConfig(ConfChange) returns (RaftResponse) {}
  rpc SendMessage(Message) returns (RaftResponse) {}
  rpc SendProposal(Proposal) returns (RaftResponse) {}
  rpc SendQuery(Query) returns (RaftResponse) {}
  rpc NewPeer(NewPeerRequest) returns (RaftResponse) {}
  rpc Transfer(TransferRequest) returns (RaftResponse) {}
  rpc CheckPromotable(PeerRequest) returns (PromotableResponse) {}
  rpc RemoveFollower(RemoveFollowerRequest) returns (RaftResponse) {}
}

message RemoveFollowerRequest {
  uint32 graph_id = 1;
  uint32 partition_id = 2;
  uint64 leader_id = 3;
  uint64 peer_id = 4;
}

message PeerRequest {
  uint32 graph_id = 1;
  uint32 partition_id = 2;
  uint64 peer_id = 3;
}

enum PeerType {
  Follower = 0;
  Learner =  1;
}

message PromotableResponse {
  bool promotable = 1;
}

message TransferRequest {
  uint32 graph_id = 1;
  uint32 partition_id = 2;
  uint64 leader_id = 3;
  uint64 transferee = 4;
}

message NewPeerRequest {
  uint32 graph_id = 1;
  uint32 partition_id = 2;
  uint64 peer_id = 3;
  uint64 leader_id = 4;
  string leader_addr = 5;
  PeerType peer_type = 6;
}

message ConfChange {
  uint32 graph_id = 1;
  uint32 partition_id = 2;
  uint64 peer_id = 3;
  bytes inner = 4;
}

message Message {
  uint32 graph_id = 1;
  uint32 partition_id = 2;
  uint64 peer_id = 3;
  repeated bytes inner = 4;
}

enum ResultCode {
  Ok            = 0;
  Error         = 1;
  WrongLeader   = 2;
}

message Proposal {
  uint32 graph_id = 1;
  uint32 partition_id = 2;
  uint64 peer_id = 3;
  bytes inner = 4;
}

message Query {
  uint32 graph_id = 1;
  uint32 partition_id = 2;
  uint64 peer_id = 3;
  bytes inner = 4;
}

message IdRequestReponse{
  ResultCode code = 1;
  bytes data = 2;
}

message Empty {
  uint32 graph_id = 1;
  uint32 partition_id = 2;
}

message Entry {
  uint64 key    = 1; 
  string value  = 2;
}

message RaftResponse {
  bytes inner = 2;
}


```