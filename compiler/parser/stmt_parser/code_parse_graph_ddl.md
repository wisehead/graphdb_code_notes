#1.parse_graph_ddl

```
parse_graph_ddl
--#map(rule!{#parse_show_graphs}, |_| GraphDDL::ShowGraphs) |
--#map(rule!{#parse_create_graph}, GraphDDL::CreateGraph) |
--#map(rule!{#parse_desc_graph}, GraphDDL::DescGraph) |
--#map(rule!{#parse_use_graph}, GraphDDL::UseGraph) |
--#map(rule!{#parse_clear_graph}, GraphDDL::ClearGraph) |
--#map(rule!{#parse_drop_graph}, GraphDDL::DropGraph) |
--#map(rule!{#parse_rename_graph}, GraphDDL::RenameGraph)

```