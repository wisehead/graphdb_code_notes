#1.struct IdPool

```rust
pub struct IdPool<T, P>
where
    T: Ord + Clone + std::ops::AddAssign + From<u32> + Default,
    P: IdApplier<T>,
{
    pub pool: Mutex<IdMemPool<T>>,
    pub source: P,
}
```