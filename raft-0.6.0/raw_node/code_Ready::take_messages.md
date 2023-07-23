#1.Ready::take_messages

```
Ready::take_messages
--if !self.is_persisted_msg {
            self.light.take_messages()
        } else {
            Vec::new()
        }
```

#2.caller

- on_ready