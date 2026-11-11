# k8sman-plugins

Community plugins for [k8sman](https://github.com/matty234/k8sman): a
`plugin.yaml` that adds columns, inspector panels, alerts and actions for a
Kubernetes CRD, with no code. Browse them at
<https://k8sman.dev/plugins>; k8sman installs them from the signed index at
<https://matty234.github.io/k8sman-plugins/index.json>.

Included: `karpenter`, `flux`, `crossplane`, `cloudnative-pg`,
`external-secrets`, `cert-manager`, `kyverno` (these three were bundled
with k8sman up to 0.2.16) and `kubevirt`.

## Submitting a plugin

1. Read the [plugin guide](https://github.com/matty234/k8sman/blob/main/docs/PLUGINS.md).
2. Add `plugins/<id>/` with `plugin.yaml`, a `README.md` that says what the
   plugin does and what it needs, an optional `icon.png`, and a `fixtures/`
   folder with objects and snapshots. Set `minAppVersion`.
3. Check it with `k8sman-server plugin validate plugins/<id>` and
   `k8sman-server plugin test plugins/<id>` (`plugin new <id> plugins` starts one).
4. Open a pull request. CI runs both commands against the latest k8sman and
   the oldest supported release.

Only top-level `.yaml`, `.md`, `.png` and `.svg` files are packaged (at most
1 MiB); `fixtures/` stays in this repo.

## Review

- Every change needs a review from a code owner (see `CODEOWNERS`).
- A pull request that changes a `permissions` block gets the `permissions`
  label and is reviewed more closely: what a plugin reads, patches or runs is
  what users are asked to consent to.
- A new version needs a new `version` in `plugin.yaml`.
- A broken version is withdrawn by adding `<id>@<version>` to `revoked.txt`.

## Publishing

On every merge to `main`, and weekly, CI packs each plugin, writes
`index.json`, signs it (`index.json.sig`) and publishes the result to GitHub
Pages. The `expires` date is 30 days ahead, so the weekly run keeps it fresh.

## Schema

`schema/` is for the plugin JSON Schema. Generate the current one with
`k8sman-server plugin schema > schema/plugin.v1.json`; editors use it for
completion (see the first line of each `plugin.yaml`).

## License

MIT, see `LICENSE`. Plugins are contributed under the same license.
