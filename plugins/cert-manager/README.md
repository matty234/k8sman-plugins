# cert-manager

[cert-manager](https://cert-manager.io) (`cert-manager.io`), with a
**cert-manager** section in the sidebar and icons for its kinds. Up to
k8sman 0.2.16 this plugin was bundled with the app; it keeps the id
`cert-manager`, so its on/off switch and settings carry over. A short,
commented version is k8sman's teaching example,
[`examples/plugins/cert-manager`](https://github.com/matty234/k8sman/tree/main/examples/plugins/cert-manager).

- **Certificates:** Ready, Issuer and Expires (time left) columns; a
  Certificate section with expiry warnings, the secret and issuer as links,
  the issuer's own status and the expiry Prometheus reports; the
  certificate's **Secret** (name, type, keys: never its values) and its
  **CertificateRequests**; DNS names, private key settings and conditions.
- **Actions on Certificates:** **Renew** and **cmctl status** run `cmctl`
  on your computer, in the dock; **Set renewal time…** and **Private key
  rotation…** change the Certificate (a form, then a dry run showing the
  change, then your confirmation).
- **Alerts:** Certificates expired, expiring within 14 days, or not ready;
  Issuers and ClusterIssuers not ready.
- **CertificateRequests:** Approved and Ready columns; issuer, requester,
  owner links and conditions.
- **Issuers and ClusterIssuers:** Type and Server columns; ACME, CA and
  Vault details and the ACME solvers.

## Permissions

Reads Certificates, CertificateRequests, Issuers, ClusterIssuers and
Secrets (names and keys only), and queries Prometheus for the expiry
metric. Runs `cmctl` on this computer, asking first each time with the
command shown. Changes Certificates, each time with a dry run and your
confirmation. Actions are hidden on read-only contexts.

The shell actions need [`cmctl`](https://cert-manager.io/docs/reference/cmctl/)
on your PATH (the dock says so when it is missing); the Expiry
(Prometheus) field needs k8sman's Prometheus integration and cert-manager's
metrics.

## Without a cluster

```sh
k8sman-server plugin test plugins/cert-manager
k8sman-server plugin render plugins/cert-manager plugins/cert-manager/fixtures/certificate-expiring.yaml
```

`fixtures/test.yaml` fixes the time, the context and a metric answer.
