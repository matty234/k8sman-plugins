# CloudNativePG

Read-only view of [CloudNativePG](https://cloudnative-pg.io) PostgreSQL
clusters (`postgresql.cnpg.io`), with a **CloudNativePG** section in the
sidebar.

**Cluster**

- Columns: **Ready** (ready / desired instances), **Status** (`Healthy`,
  `Progressing: <phase>` or `Error: <phase>`), **Postgres** (the image tag,
  or the major version), **Storage** and **Last Backup**.
- Panel:
  - **Cluster**: the phase and its reason, the primary and how long it has
    been primary, the timeline, image or image catalog, storage and WAL
    storage, and the `-rw`, `-ro` and `-r` services. It also says when the
    primary is failing, a switchover or failover is under way, volumes are
    unusable, dangling or resizing, or managed roles can't be reconciled.
  - **Instances**: each instance with its role (primary or replica), its
    state as the operator reports it (healthy, replicating, failed), its
    pod's readiness, restarts, node and timeline.
  - **Replication and HA**: replicas, synchronous replication, HA
    replication slots, primary update strategy, failover delay, PDB,
    anti-affinity, the nodes used and the replica-cluster source.
  - **Backups and WAL archiving**: whether continuous archiving works, the
    WAL archiver (the Barman Cloud plugin or in-tree `barmanObjectStore`),
    the plugin's ObjectStore, retention, the last successful and failed
    backups, the first recoverability point (from the cluster, or the
    ObjectStore's recovery window), the cluster's ScheduledBackups and its
    five latest Backups.
  - **Certificates**: each certificate's expiry from
    `status.certificates.expirations`.
  - **Poolers** and **Databases** for the cluster, PostgreSQL parameters
    (collapsed) and the conditions.
- Alerts:
  - cluster not healthy for 5 minutes (error);
  - instances not all ready for 5 minutes (warning);
  - continuous archiving failing (error);
  - last backup failed (error);
  - no successful backup for 2 days, on clusters that take backups
    (warning);
  - a certificate expiring within 6 days (warning). CloudNativePG renews
    its own certificates 7 days before they expire.

  Hibernated clusters (`cnpg.io/hibernation=on`) are not alerted on.
- Status line: `Clusters: 4 · not healthy: 1 · archiving failing: 0 ·
  backup failed or overdue: 0`.

**Backup**: phase, start time and duration columns; a panel with the
cluster, the ScheduledBackup that made it, method and plugin, the instance
it ran on, its WAL range and LSNs, and the error of a failed one.

**ScheduledBackup**: schedule, method, next run and suspended columns; a
panel with the schedule and its ten latest Backups.

**Pooler**: pool mode, instances and paused columns; a panel with its type,
ready PgBouncer pods (from its Deployment), its Service, its pods and the
PgBouncer parameters.

**Database**, **Publication** and **Subscription**: whether the operator
applied them, with its message when it didn't (and an alert); a Database's
extensions and schemas.

**ImageCatalog** and **ClusterImageCatalog**: the major versions and their
images.

**ObjectStore** (`barmancloud.cnpg.io`, the Barman Cloud plugin):
destination, retention, compression, each server's recovery window, and
its configuration (credentials show as Secret names and keys only).

**Pods** of a cluster (label `cnpg.io/cluster`) or of a pooler
(`cnpg.io/poolerName`) get a CloudNativePG section after their status: the
cluster and its phase, the role (primary or replica), the instance's state
and timeline, or the pooler.

## Permissions

Reads the CloudNativePG kinds above, `barmancloud.cnpg.io` ObjectStores,
Pods (a cluster's instances, a pooler's pods) and Deployments (a pooler's).
It reads no Secrets, changes nothing and runs no commands.
