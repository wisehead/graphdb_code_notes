#1.MvccCollector::apply_insert_vertex_for_topology

```
MvccCollector:: apply_insert_vertex_for_topology
--let delta = TopologyDelta::default()
            .set_inner(TopologyDeltaInner::InsertVertex)
            .build();
--self.topology
            .entry(vertex_key.clone())
            .or_insert_with(|| (DoublyLinkedList::default(), false))
            .0
            .push_front(delta);

```