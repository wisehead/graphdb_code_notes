#1.struct QoContext

```rust
#[derive(Default, Debug, Clone)]
pub struct QoContext {
    pub(crate) graph_id: GraphId,
    next_plan_node_id: Arc<RefCell<PlanNodeId>>, // the unique operator id in the plan, it's auto-incremented.
    pub(crate) available_aliases: Vec<(String, Expression)>,
    pub(crate) schema_cache: HashMap<String, SchemaInfo>, /* type_name to Schema */
    pub(crate) alias_to_types: HashMap<String, Vec<String>>,
    pub(crate) type_to_aliases: HashMap<String, HashSet<String>>, /* type name to alias names */
    pub(crate) hint_context: HintContext,
    // separated context for subquery blocks (subquery in set operator(union,...))
    sub_qo_contexts: HashMap<PlanNodeId, QoContext>,
    // at a moment, only a plangen context is avaiable(a parent context or a sub context)
    is_sub_qo_context_being_used: bool,
    //whether the query run in async mode, in async mode, the ap result will be saved temporarily
    pub(crate) is_async: bool,
    pub(crate) job_id: Option<JobId>,
    pub(crate) is_fetch_result_from_cache: bool,
    // In a graph, Vertex/Edge Ids are Unique, Property Ids are unique
    // so privileges is map: GraphId -> (PrivilegeType, VertexEdgePrivilegesMap, PropertIdPrivilegesMap)
    // pub(crate) user_privileges: UserPrivileges,
}

```