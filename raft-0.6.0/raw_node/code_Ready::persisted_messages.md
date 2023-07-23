#1.Ready::persisted_messages

```
Ready::persisted_messages
--if self.is_persisted_msg {//follower message after HardState
            self.light.messages()
        } else {
            &[]
        }
```