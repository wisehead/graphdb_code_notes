#1.PlanVisitor::visit

```
PlanVisitor::visit
--self.pre_visit(op)?;
--// visit children before current node: post-order.
--for child in &op.children {
----self.visit(child)?;
------PlanVisitor::visit
--self.visit_current(op)?;
----PlanVisitor::visit_current
------PlanVisitor::visit_plan_node
--------PlanVisitor::visit_insert
----------DependentObjects::visit_insert
--self.post_visit(op)?;
```