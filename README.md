# DevCloud releases

Public, checksum-verified DevCloud binaries for Linux, macOS, and 64-bit Windows. The application
source stays in the private `hapwi/devcloud` repository; this repository contains only release
binaries, checksums, and the workflow that publishes the GitHub Release page.

See [CHANGELOG.md](CHANGELOG.md) for the features, fixes, and security changes included in every
public release.

## Release channels

Before `v1.0.0`, the newest beta-tagged build is the current public DevCloud release and is featured
as **Latest**. Starting with `v1.0.0`, stable versions remain **Latest** while development builds for
the next version, such as `v1.0.1-beta.1` or `v1.0.1-rc.1`, are published as prereleases. Promoting a
tested candidate creates the matching stable release, such as `v1.0.1`.

## Add a computer

1. Sign in at [www.dotflag.dev/dashboard](https://www.dotflag.dev/dashboard).
2. Select **Add machine** and create a one-time device request.
3. Choose **macOS / Linux** or **Windows**.
4. Run the generated command on the computer being added.
5. Approve the request in the browser opened on that computer.

The generated command includes a single-use pairing secret. Do not copy that command to another
computer or share it with anyone.

## Install or update an already paired computer

Linux and macOS:

```sh
curl -fsSL https://www.dotflag.dev/install.sh | sh
```

Windows PowerShell:

```powershell
irm https://www.dotflag.dev/install.ps1 | iex
```

The installer detects the platform, downloads the version selected by the DevCloud control plane,
verifies its SHA-256 checksum, replaces the existing binary, and restarts the background service.

After installation:

```text
devcloud --version
devcloud status
```

## Share a local project

Start the project normally, then expose its HTTP port:

```text
bun dev
devcloud expose 3000 app
```

DevCloud returns a private HTTPS link. Only a computer enrolled in the same cloud can open it; being
signed into the dashboard in a browser does not make that browser an enrolled device.

## Update from the CLI

```text
devcloud update --check
devcloud update
```

## Release assets

Each release contains:

- `devcloud-linux-x86_64` and `devcloud-linux-aarch64`
- `devcloud-macos-x86_64` and `devcloud-macos-aarch64`
- `devcloud-windows-x86_64.exe`
- one `.sha256` file for every binary

Windows 10/11 x64 is native. Windows 11 ARM uses Windows' x64 compatibility support because the
pinned Cloudflare tunnel client does not currently provide a native Windows ARM64 executable.
