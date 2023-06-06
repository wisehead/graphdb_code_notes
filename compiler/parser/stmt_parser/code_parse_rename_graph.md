#1.parse_rename_graph

```
parse_rename_graph
--rule! {
            RENAME ~ GRAPH ~ #parse_ident ~ TO ~ #parse_ident
        },
        |v| RenameGraph {
            from_name: v.2,
            to_name: v.4,
        },
```