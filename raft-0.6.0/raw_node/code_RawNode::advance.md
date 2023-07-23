#1.RawNode::advance

```
    /// Advances the ready after fully processing it.
    ///
    /// Fully processing a ready requires to persist snapshot, entries and hard states, apply all
    /// committed entries, send all messages.
    ///
    /// Returns the LightReady that contains commit index, committed entries and messages. [`LightReady`]
    /// contains updates that only valid after persisting last ready. It should also be fully processed.
    /// Then [`Self::advance_apply`] or [`Self::advance_apply_to`] should be used later to update applying
    /// progress.
RawNode::advance
--let applied = self.commit_since_index;
        let light_rd = self.advance_append(rd);
        self.advance_apply_to(applied);
        light_rd
```