#1.enum PlanNode

```rust
pub enum PlanNode {
    ApCall(ApCallPlan),
    ExportInto(ExportIntoPlan),
    Union(UnionPlan),
    Intersect(IntersectPlan),
    Except(ExceptPlan),
    Jaccard(JaccardPlan),
    // Query
    Project(ProjectPlan), // return statement
    Distinct(DistinctPlan),
    Limit(LimitPlan),
    Sort(SortPlan),
    Filter(FilterPlan),             // post-filter
    VertexFilter(VertexFilterPlan), // dest vertex of a hop
    Expand(ExpandPlan),             // single hop
    VarExpand(VarExpandPlan),       // multiple hops on same Edge and filter
    Traverse(TraversePlan),         // single hop plus path
    VarTraverse(VarTraversePlan),   // multiple hops on same Edge and filter, plus path
    VertexScan(VertexScanPlan),
    VertexIndexScan(VertexIndexScanPlan),
    EdgeScan(EdgeScanPlan),
    EdgeIndexScan(EdgeIndexScanPlan),
    Materialize(MaterializePlan),
    GroupBy(GroupByPlan),
    // DML
    Insert(InsertPlan),
    Delete(DeletePlan),
    Set(SetPlan),
    // DCL
    CreateUser(CreateUserPlan),
    ShowUser(ShowUserPlan),
    DropUser(DropUserPlan),
    AlterUser(AlterUserPlan),
    CreateRole(CreateRolePlan),
    DropRole(DropRolePlan),
    ShowRoles(ShowRolesPlan),
    ShowUserRoles(ShowUserRolesPlan),
    RenameRole(RenameRolePlan),
    GrantRoleToUser(GrantRoleToUserPlan),
    GrantPrivilgeToRole(GrantPrivilgeToRolePlan),
    RevokePrivilgeToRole(RevokePrivilgeToRolePlan),
    RevokeRoleFromUser(RevokeRoleFromUserPlan),
    ShowRolePrivileges(ShowRolePrivilegesPlan),
    ShowInfra(ShowInfraPlan),

    #[default]
    Dummy,
}
```