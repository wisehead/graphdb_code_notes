#1.message ReplyMsg

```proto
message ReplyMsg {
  common.ReplyStatus status = 1;
  string msg = 2;
  optional bytes ret_data = 3;
}

```