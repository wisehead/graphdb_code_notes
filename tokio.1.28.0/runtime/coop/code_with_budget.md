#1.with_budget

```
with_budget
--let maybe_guard = context::budget(|cell| {
        let prev = cell.get();
        cell.set(budget);

        ResetGuard { prev }
    });

```

#2.caller

```
- budget

```