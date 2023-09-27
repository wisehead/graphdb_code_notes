#1.LinkBuffer::advance_tail_until

```
LinkBuffer::advance_tail_until
--let mut tail = self.get_tail();
--let mut from = tail;
--let mut retry = 0;
--loop {
            let index = self.slot_index(from);
            let next = self.link_buffer[index].load(Ordering::Acquire);

            if next >= tail + self.capacity as u64 {
                // either we wrapped and tail was advanced meanwhile,
                // or there is link start_lsn -> end_lsn of length >= m_capacity
                tail = self.get_tail();
                if tail != from {
                    from = tail;
                    continue;
                }
            }

            if next <= tail || stop_func(tail, next) {
                // nothing to advance for now
                return false;
            }

            // try to lock as storing the end
            if Ok(next)
                == self.link_buffer[index].compare_exchange(
                    next,
                    tail,
                    Ordering::AcqRel,
                    Ordering::Acquire,
                )
            {
                // it could happen, that after thread read position = m_tail.load(),
                // it got scheduled out for longer; when it comes back it might still
                // see the link going forward in that slot but m_tail could have been
                // already advanced forward (as we do not reset slots when traversing
                // them); thread needs to re-check if m_tail is still behind the slot.
                tail = self.get_tail();
                if tail == from {
                    // confirmed. can advance tail exclusively
                    tail = next;
                    break;
                }
            }

            retry += 1;
            if retry > max_retry {
                // give up
                return false;
            }

            // UT_RELAX_CPU();
            tail = self.get_tail();
            if tail == from {
                // no progress?
                return false;
            }
            from = tail;
--}

--loop {
            let mut next: u64 = 0;

            let stop = self.next_position(tail, &mut next);

            if stop || stop_func(tail, next) {
                break;
            }

            tail = next;
--}
--self.set_tail(tail);
```