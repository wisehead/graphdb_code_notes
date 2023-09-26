#1.LinkBuffer::advance_tail

```
LinkBuffer::advance_tail
--let stop_condition = |_prev, _next| false;
--self.advance_tail_until(&stop_condition, 0);

```