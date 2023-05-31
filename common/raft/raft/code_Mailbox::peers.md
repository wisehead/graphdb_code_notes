#1.Mailbox::peers

```
Mailbox::peers
--self.peers
            .iter()
            .map(|p| {
                let (id, _) = p.key();
                (*id, p.value().clone())
            })
            .collect::<Vec<_>>()
```