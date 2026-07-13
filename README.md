# DevCloud

**Your development environment, everywhere.**

DevCloud turns the computers you already own into a private development cloud. Open local projects
from another computer or your phone, connect to your machines over SSH, and keep building without
moving your code or exposing your network.

[Get started](https://www.dotflag.dev) · [Open the dashboard](https://www.dotflag.dev/dashboard) ·
[See what’s new](CHANGELOG.md)

## Your machines. One private cloud.

DevCloud gives your local development services stable, private HTTPS links that travel with you.
Keep your existing setup, framework, editor, and hardware—DevCloud handles the secure connection.

- **Build with what you already use.** Next.js, Vite, Astro, Rails, local APIs, and anything else
  that serves HTTP all work the same way.
- **Open localhost from anywhere.** Reach a project from another enrolled computer or a paired phone
  without router configuration or port forwarding.
- **Connect to your computers.** Use secure SSH between enrolled machines through DevCloud’s managed
  outbound connection.
- **Stay private by default.** Projects are available only to devices you explicitly trust, and
  access can be revoked from the dashboard.

## Start in a few minutes

1. Sign in to the [DevCloud dashboard](https://www.dotflag.dev/dashboard).
2. Select **Add machine** and choose your operating system.
3. Run the generated one-time command on the computer you want to add.
4. Approve the request and start your project normally.

Then expose its local port:

```sh
# Run your app as usual
pnpm dev

# Give its local port a private DevCloud link
devcloud expose 3000 web
```

DevCloud returns a private HTTPS address for your project. No deployment, repository migration, or
changes to your app are required.

## Take your projects with you

Pair a phone to open private project links on mobile:

```sh
devcloud mobile pair
```

Connect from one enrolled computer to another over SSH:

```sh
devcloud connect home-server
```

Phones can open private HTTP projects. SSH remains restricted to enrolled computers, where your
normal SSH keys and host verification continue to protect the session.

## Private by design

DevCloud is built around explicit device trust rather than public links.

- Connections leave your computer through managed outbound tunnels; inbound ports stay closed.
- Pairing requests are short-lived, single-use, and require approval.
- Project and SSH access are limited to devices in the same private cloud.
- Removing a machine or phone revokes its access.
- Updates are checksum-verified against a signed release manifest before installation.

## Install or update DevCloud

Already have a paired machine? Install or repair the background agent with the official installer.

Linux and macOS:

```sh
curl -fsSL https://www.dotflag.dev/install.sh | sh
```

Windows PowerShell:

```powershell
irm https://www.dotflag.dev/install.ps1 | iex
```

Check your connection or install the newest release at any time:

```sh
devcloud status
devcloud update --check
devcloud update
```

## Platform support

DevCloud provides native agents for:

- Linux on x86_64 and ARM64
- macOS on Apple silicon and Intel
- Windows 10/11 on x86_64

Windows 11 on ARM can run the x86_64 agent through Windows compatibility support.

## About this repository

This is DevCloud’s official public download channel. Each release includes the platform binaries,
individual SHA-256 checksums, a signed release manifest, and customer-facing release notes in the
[changelog](CHANGELOG.md).

DevCloud is currently in beta and improving quickly. The newest published beta is the recommended
version until the first stable release.
