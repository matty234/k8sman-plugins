# Flux

Read-only view of [Flux](https://fluxcd.io): `Kustomization`,
`HelmRelease`, `GitRepository` and `HelmRepository`.

- A **Ready** column (the Ready condition's reason when it is not ready, or
  `Suspended`), a **Revision** column and a **Suspended** column.
- A panel with the revision, source, path or chart, a Ready / Suspended
  badge and the failing condition's message.
- An alert for each object whose Ready condition is False. Suspended
  objects are not alerted on.

Permissions: reads the four kinds above. It changes nothing and runs no
commands.
