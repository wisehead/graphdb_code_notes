#1.HashStore::apply

```
HashStore::apply
--let message: Message = deserialize(message).unwrap();
--let message: Vec<u8> = match message {
----Message::Insert { key, value } => {
                let mut db = self.data.write().unwrap();
                let v = serialize(&value).unwrap();
                db.insert(key, value);
                v
            }
----_ => Vec::new(),
```

#2.caller

-- handle_normal