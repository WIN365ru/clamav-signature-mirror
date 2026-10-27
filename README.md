# ClamAV signature mirror

Official signed antivirus databases for disposable torrent scan workers.

The GitHub Actions workflow updates every six hours using Cisco Talos cvdupdate. It verifies CVD signatures with ClamAV, rejects daily definitions older than 48 hours, and publishes a complete snapshot before marking it latest. Three completed snapshots are retained. Failed updates leave the last good release intact.

Set the scanner configuration malware.signature_mirror to:

    https://github.com/WIN365ru/clamav-signature-mirror/releases/latest/download

The release contains main.cvd, daily.cvd, bytecode.cvd, manifest.json (build times, versions and SHA-256 hashes), and updater-state.json. Workers use FreshClam PrivateMirror mode with database verification enabled and independently reject stale definitions.

Run Update signed ClamAV mirror from the Actions tab to trigger an update manually. Shared GitHub runner addresses can be rate-limited by the upstream CDN; inspect a successful run and the manifest before enabling production scans.

No torrent samples, Telegram credentials, Portainer credentials, or VirusTotal API keys belong in this repository. Public release assets require no GitHub token in scan workers. The publisher uses the scoped automatic GITHUB_TOKEN, not a personal access token.

References:

- https://docs.clamav.net/appendix/CvdPrivateMirror.html
- https://github.com/Cisco-Talos/cvdupdate
