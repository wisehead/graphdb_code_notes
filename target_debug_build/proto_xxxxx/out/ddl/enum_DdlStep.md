#1.enum DdlStep

```rust

pub enum DdlStep {
    KStepForward = 0,
    KStepLock = 1,
    KStepPrepare = 2,
    KStepCommit = 3,
    KStepCleanup = 4,
    KStepRollback = 5,
}
```