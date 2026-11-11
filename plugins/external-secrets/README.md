# External Secrets

[External Secrets Operator](https://external-secrets.io)
(`external-secrets.io`), with an **External Secrets** section in the
sidebar. Up to k8sman 0.2.16 this plugin was bundled with the app; it keeps
the id `external-secrets`, so its on/off switch and settings carry over.

- Columns: ExternalSecret Store, Refresh, Status, Last Sync and Target;
  ClusterExternalSecret External Secret, Namespaces, Failed, Refresh and
  Status; SecretStore and ClusterSecretStore Provider, Status and
  Capabilities; PushSecret Stores, Status and Last Sync. The CRD printer
  columns they repeat are hidden.
- Panels that replace the generic one:
  - **ExternalSecret**: sync status (the Ready reason; a callout titled with
    it when not ready), the store (with its status), the
    ClusterExternalSecret that made it, the target Secret (a warning while
    it doesn't exist; its keys, never its values), the data mapping
    (`data` and `dataFrom`) and the template.
  - **ClusterExternalSecret**: status, store, namespace selection,
    provisioned and failed namespaces.
  - **SecretStore** and **ClusterSecretStore**: status, provider and its
    settings as `path → value` rows (Secret and ServiceAccount references
    are links with their name and key), conditions, and the ExternalSecrets
    that use the store.
  - PushSecret keeps the generic panel.
- Alerts: ExternalSecrets **not synced** (warning) and **not synced for
  over a day** (critical), from the Ready condition and its last
  transition.
- Status line: `ExternalSecrets: 12 · not synced: 2`.
- **Refresh now** on ExternalSecrets and PushSecrets: a merge patch that
  sets the `force-sync` annotation, with a dry run and a confirmation,
  never on read-only contexts.

## Permissions

Reads the External Secrets kinds above and Secrets (names and keys only,
never values). Changes ExternalSecrets and PushSecrets (the refresh
annotation), each time with your confirmation. Runs no commands.

## Without a cluster

```sh
k8sman-server plugin test plugins/external-secrets
```
