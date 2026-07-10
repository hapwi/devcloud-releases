# DevCloud changelog

Public release notes for the DevCloud CLI and device agent. DevCloud is currently in beta, so commands
and behavior may continue to evolve before the first stable release.

## 0.0.1-beta.20260710.15

### Improved

- Stream machine, service, and security activity changes to signed-in dashboards through an
  authenticated Convex subscription instead of five-second machine polling.
- Detect local listener changes every two seconds while sending backend updates only when services
  change, preserving the normal one-minute presence heartbeat.

### Security

- Derive realtime dashboard ownership exclusively from the verified Clerk identity inside Convex and
  return only the existing public machine projection, never device tokens or tunnel credentials.

## 0.0.1-beta.20260710.14

### Improved

- Added a direct link to the machines dashboard after approving a CLI login.
- Replaced the plain device-verification handoff with a polished DevCloud connection screen and a
  clear manual fallback while the private project opens.

## 0.0.1-beta.20260710.13

### Added

- Require both an enrolled device and an active `devcloud login` session before issuing HTTP or SSH
  project-access grants.
- Show device enrollment, account login, project authorization, session expiration, local agent, and
  tunnel state in the modernized `devcloud status` output.

### Security

- Bind private-link browser sessions to the approving CLI session, so logout revokes linked browser
  access and expired or removed sessions fail on the next request.
- Re-authorize older CLI sessions through the normal `devcloud login` flow to add the new
  `projects:access` scope without re-enrolling the computer.

## 0.0.1-beta.20260709.12

### Fixed

- Removed the automatic loopback probe from private-link 404 pages, avoiding Chrome's local-network
  permission prompt. Device verification now starts only when the visitor selects its link.

## 0.0.1-beta.20260709.11

### Fixed

- Excluded the DevCloud agent and its managed `cloudflared` process from detected project services,
  so internal loopback listeners such as the Cloudflare metrics endpoint are not shown in the dashboard.

## 0.0.1-beta.20260709.10

### Fixed

- Allowed the private-link 404 gate to probe only the fixed DevCloud loopback agent endpoint, so an
  enrolled same-cloud device can reveal the Verify button without weakening the page's default-deny
  Content Security Policy.

## 0.0.1-beta.20260709.9

### Added

- Added `devcloud login`, `logout`, `account`, and `machines` for browser-approved CLI management.
- Added 30-day, read-only CLI sessions with one-time browser approval and remote logout revocation.
- Added durable 30-day private-link browser sessions that survive agent restarts.

### Improved

- Private links now return a generic 404 until a loopback DevCloud agent proves the viewing computer
  belongs to the same cloud; only then is device verification shown.
- Existing readable machine routes migrate automatically to globally unique 128-bit routing IDs
  without re-pairing the computer.
- Added clearer recovery guidance when an older CLI cannot open an SSH authorization tunnel.

### Security

- CLI and private-link session secrets are stored only as SHA-256 hashes in the control plane.
- CLI login uses a 256-bit proof-bound credential, ten-minute approval request, explicit Clerk approval,
  scoped access, same-origin approval checks, and rate limits.
- Removing either enrolled machine rejects its private-link sessions on the next request or WebSocket
  handshake.
- Machine names remain friendly dashboard/CLI aliases and are never reused as public DNS identities.

## 0.0.1-beta.20260709.8

### Improved

- Added a compact progress bar for CLI updates, including download, checksum verification,
  installation, and service restart stages.
- Added clearer up-to-date and successful-update messages.
- Silenced harmless cleanup warnings from obsolete Linux and macOS background services.
- Changed macOS upgrades to restart the existing LaunchAgent in place, avoiding repeated background
  item registration during routine updates.

## 0.0.1-beta.20260709.7

### Added

- Added `devcloud connect <machine>` for secure SSH between enrolled computers.
- Added short-lived, single-use SSH access grants restricted to online devices in the same cloud.
- Added strict SSH host-key pinning and explicit approval for legitimate host-key changes.
- Added SSH readiness details and readable SSH session events to the dashboard.

### Security

- SSH travels through the target's outbound managed tunnel; raw port 22 is never exposed publicly.
- DevCloud does not collect private SSH keys or account passwords. OpenSSH continues to perform normal
  user authentication.

## 0.0.1-beta.20260709.6

### Fixed

- Fixed Unix self-updates so the background service always keeps the stable DevCloud executable path.
- Deduplicated multiple detected HTTP listeners belonging to the same development-server process.

## 0.0.1-beta.20260709.5

### Improved

- Simplified private project-link management and HTTP development-server detection.
- Made enrolled-device authorization pages persistent instead of redirecting to an unavailable local
  URL after a failed handoff.
- Reworked security activity into readable device-to-device access events.

## 0.0.1-beta.20260709.4

### Fixed

- Added safe migration for computers enrolled with the earlier DevCloud credential layout.
- Preserved existing device enrollment while moving to the current agent configuration and service.

## 0.0.1-beta.20260709.3

### Added

- Added native Windows x64 CLI releases, PowerShell installation, checksum verification, and an
  on-logon background task.

## 0.0.1-beta.20260709.2

### Security

- Moved public downloads into the dedicated `devcloud-releases` repository so application source can
  remain private.
- Added a SHA-256 checksum file for every supported binary.

## 0.0.1-beta.20260709.1

### Added

- Introduced dated beta versioning and the checksum-verified `devcloud update` release channel.
