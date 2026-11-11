# Karpenter

Read-only view of [Karpenter](https://karpenter.sh) (`karpenter.sh/v1`).

- **NodePool**: Ready, Nodes, Limits and Consolidation columns; a panel with
  resources in use, node class and conditions; an alert when a NodePool is
  not ready.
- **NodeClaim**: Ready, Node, NodePool, instance type and capacity-type
  columns; a panel with the launched / registered / initialized steps; an
  alert for a NodeClaim that is still not ready after 15 minutes.

Permissions: reads NodePools and NodeClaims. It changes nothing and runs no
commands.
