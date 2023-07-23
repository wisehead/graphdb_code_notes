#1.Ready::messages

```
    /// Messages specifies outbound messages to be sent.
    /// If it contains a MsgSnap message, the application MUST report back to raft
    /// when the snapshot has been received or has failed by calling ReportSnapshot.
Ready::messages
--if !self.is_persisted_msg {//注意这里是没有persisted
            self.light.messages()
        } else {
            &[]
        }

```