# KubeVirt

[KubeVirt](https://kubevirt.io) virtual machines and the [CDI](https://github.com/kubevirt/containerized-data-importer)
objects around them.

- **Kinds** (a "KubeVirt" section in the sidebar): `VirtualMachine`,
  `VirtualMachineInstance`, `DataVolume`, `VirtualMachineInstanceMigration`,
  `VirtualMachineSnapshot`, `VirtualMachineRestore`, instance types and
  preferences (cluster and namespaced).
- **VirtualMachine** table: Status (`printableStatus`), Ready, Run strategy
  (`spec.runStrategy`, or the legacy `spec.running`) and Resources (the
  instance type, else vCPUs and memory). The panel shows the status and
  conditions, pending state change requests, the VirtualMachineInstance
  (phase, node, IPs, guest OS), the launcher pod, disks and volumes joined
  with their DataVolume's phase and progress, networks (with the IPs and
  MACs the instance reports, and Multus attachments linked), the instance
  type and preference, the VM's snapshots, and CPU, memory and network usage.
- **VirtualMachineInstance**: phase, node, IP, Ready and live-migratable;
  interfaces, guest OS (or a note that there is no guest agent), migration
  state, owner VM, launcher pod and usage.
- **DataVolume**: phase, progress, a short source (`http`, `registry`, `pvc`,
  `blank`, `upload`, ...), size and storage class.
- **Alerts**: a VM that should be running but has not been ready for 5
  minutes, a VM in an error status (`ErrorUnschedulable`, `ErrImagePull`,
  `ImagePullBackOff`, `CrashLoopBackOff`, `DataVolumeError`, ...), a paused
  VM, a failed DataVolume and a failed migration. The status line counts VMs
  (running, paused, error) and DataVolumes.
- **Actions** on a VirtualMachine: **Start** and **Stop** patch
  `spec.runStrategy` (`Always` / `Halted`, or `spec.running` for a VM that
  still uses it), after a dry run you confirm. Stop is marked dangerous.
- **Restart** and **Live migrate** on a VirtualMachine, and **Pause** /
  **Unpause** on a VirtualMachineInstance, call KubeVirt's subresource API
  (`subresources.kubevirt.io`) with your credentials. **Snapshot…** creates a
  `VirtualMachineSnapshot` of the VM after a dry run. The serial console is
  built into k8sman (**Serial console** on a running VM or VMI).
- **VNC** runs `virtctl vnc` on your computer, which opens a local viewer, so
  it needs [`virtctl`](https://kubevirt.io/user-guide/user_workloads/virtctl_client_tool/)
  on your PATH.
- **Templates** for the New Resource editor: a VM from a containerDisk, a VM
  with a DataVolumeTemplate that imports a cloud image, DataVolumes (HTTP
  import, blank), a snapshot, a restore, an instance type and a migration.
- **Usage** needs the Prometheus integration scraping KubeVirt
  (`kubevirt_vmi_*` metrics, labelled `name` and `namespace`).

Permissions: reads the kinds above and Pods, patches `VirtualMachine`, calls
the `restart`, `migrate`, `pause` and `unpause` subresources, creates
`VirtualMachineSnapshot`s, runs `virtctl` (VNC only), and queries Prometheus.
Needs k8sman 0.2.20 or later.
