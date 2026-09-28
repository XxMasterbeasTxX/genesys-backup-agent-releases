# Genesys backup agent — releases

Windows builds of the **Genesys backup agent**, which makes backups of a Genesys Cloud
organisation in the organisation's own environment on orders from the Genesys Admin App
(Backup › Backups).

This repository holds **release files only** — no source code, no secrets and no customer
data. Each release has:

- `genesys-backup-agent-<version>-windows-amd64.zip` — the agent (a single executable),
  the pinned Terraform and Genesys provider, and `install-windows.ps1`
- `….zip.sha256` — its SHA-256 checksum

Check a download before installing:

```powershell
(Get-FileHash .\genesys-backup-agent-<version>-windows-amd64.zip -Algorithm SHA256).Hash
```

and compare it with the `.sha256` file. Then, in an elevated PowerShell in the unzipped folder:

```powershell
.\install-windows.ps1 -App https://<admin app> -Code XXXX-XXXX-XXXX `
  -Destination \fileserver\backups\genesys -Region mypurecloud.de -ClientId <backup client id>
```

The registration code comes from **Backup › Backups › Add agent** in the Admin App.
The container image is `ghcr.io/xxmasterbeastxx/genesys-backup-agent`.
