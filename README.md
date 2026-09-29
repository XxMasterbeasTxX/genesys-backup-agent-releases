# Genesys backup agent — releases

Windows builds of the **Genesys backup agent**, which makes backups of a Genesys Cloud
organisation in the organisation's own environment on orders from the Genesys Admin App
(Backup › Backups).

This repository holds **release files only** — no source code, no secrets and no customer
data. Each release has:

- `genesys-backup-agent-<version>-windows-amd64.zip` — the agent (a single executable),
  the pinned Terraform and Genesys provider, and `install-windows.ps1`
- `….zip.sha256` — its SHA-256 checksum

**The full installation guide** — a Windows machine or server, and Azure Container Apps —
is in the Admin App: **Backup › Backups › How to install the agent**.

In short, for Windows: check the download (the two values must match; the file writes it in
lower case),

```powershell
(Get-FileHash .\genesys-backup-agent-<version>-windows-amd64.zip -Algorithm SHA256).Hash
Get-Content .\genesys-backup-agent-<version>-windows-amd64.zip.sha256
```

then, in an elevated PowerShell in the unzipped folder, with a registration code from
**Backup › Backups › Add agent**:

```powershell
.\install-windows.ps1 -App https://<admin app> -Code XXXX-XXXX-XXXX `
  -Destination "\\fileserver\backups\genesys" -Region mypurecloud.de -ClientId <Admin Tool OAuth client id>
```

The client is the organisation's Admin Tool OAuth client — the same one the Admin App uses
for it. The installer asks for its secret.

The container image is `ghcr.io/xxmasterbeastxx/genesys-backup-agent`.
