#1.Partition::produce_result

```
Partition::produce_result
--let dataset = std::mem::take(&mut *self.cached_data.borrow_mut());
--*self.cached_row_num.borrow_mut() = 0;

--Result::Ok(dataset)

```