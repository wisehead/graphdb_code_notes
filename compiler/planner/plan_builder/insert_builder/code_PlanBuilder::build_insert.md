#1.PlanBuilder::build_insert

```
PlanBuilder::build_insert

```

#2.caller

```
convert_ast_to_plan
--PlanBuilder::build_ast
----PlanBuilder::build_regular_query
------PlanBuilder::build_single_query
--------PlanBuilder::build_single_part_query
----------PlanBuilder::build_updating_clauses
------------PlanBuilder::build_insert
```

#3.caller of PlanBuilder::build_single_query

```
- build_single_query//caller of build_single_query is also  PlanBuilder::build_regular_query
- PlanBuilder::build_regular_query
```



#4.caller of PlanBuilder::build_regular_query

```
- PlanBuilder::build_ast
- PlanBuilder::build_explain
```

