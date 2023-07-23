#1.RawNode::advance_append

```
RawNode::advance_append
--self.commit_ready(rd);
--self.on_persist_ready(self.max_number);
        let mut light_rd = self.gen_light_ready();
```

#2.notes

```rust
    /// Advances the ready without applying committed entries. [`Self::advance_apply`] or
    /// [`Self::advance_apply_to`] should be used later to update applying progress.
    ///
    /// Returns the LightReady that contains commit index, committed entries and messages.
    ///
    /// Since Ready must be persisted in order, calling this function implicitly means
    /// all ready collected before have been persisted.
```