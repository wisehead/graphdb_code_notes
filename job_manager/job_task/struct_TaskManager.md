#1.struct TaskManager

```rust
pub struct TaskManager {
    tasks: Mutex<HashMap<TaskId, VecDeque<Task>>>,
    cond_var: Condvar,
    error_handler: RwLock<HashMap<TaskId, Box<CallBackFn>>>,
}
```