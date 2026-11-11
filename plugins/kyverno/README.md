# Kyverno

[Kyverno](https://kyverno.io) policies (`kyverno.io`,
`policies.kyverno.io`) and the policy reports it writes (`wgpolicyk8s.io`),
with a **Kyverno** section in the sidebar. Up to k8sman 0.2.16 this plugin
was bundled with the app; it keeps the id `kyverno`, so its on/off switch
and settings carry over.

- **ClusterPolicy** and **Policy**: Action, Background, Ready and Rules
  columns; a panel with the policy's settings, its rules (type, kinds,
  message and definition), its status and the results reported for it.
- Kyverno 1.14+ kinds (ValidatingPolicy, ImageValidatingPolicy,
  MutatingPolicy, GeneratingPolicy, DeletingPolicy and PolicyException) get
  icons and the generic panel.
- **PolicyExceptions**, **CleanupPolicies** and **ClusterCleanupPolicies**
  (schedule, last execution) and **UpdateRequests** (type, policy, state):
  columns.
- **PolicyReport** and **ClusterPolicyReport**: Pass, Fail, Warn, Error,
  Skip and Scope columns; a panel with the summary and each result.
- **Policy results on any object**: a Policy results tab (under Security)
  on every object that owns a PolicyReport, as Kyverno 1.10+ writes them
  (one report per resource). Any engine that writes per-resource
  PolicyReports shows there too.
- Status line: `ClusterPolicies: 12 · not ready: 1 · Policies: 3`.

## Permissions

Reads the Kyverno kinds and policy reports above. The `"*"` entry lets it
look up the PolicyReports an object owns, for the Policy results tab. It
changes nothing and runs no commands.

## Without a cluster

```sh
k8sman-server plugin test plugins/kyverno
```
