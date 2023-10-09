#1.struct IdMemPool

```rust
pub struct IdMemPool<T>
where
    T: Ord + Clone + std::ops::AddAssign + From<u32> + Default,
{
    pub start: T,
    pub end: T,
}
```