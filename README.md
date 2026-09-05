# tercenctl distribution

Public release artefacts for `tercenctl`, the Tercen command line tool. The
source lives in the `tercen/sci` repository; this repository carries nothing
but the built binaries, published automatically by its CI.

## Getting it

The repository is public — download straight from the latest release, no
GitHub account needed:

```bash
curl -fL -o ~/.local/bin/tercenctl \
  https://github.com/tercen/tercenctl-dist/releases/latest/download/tercenctl-linux-x64
chmod +x ~/.local/bin/tercenctl
tercenctl --version
```

`gh` works too if you have it:

```bash
gh release download --repo tercen/tercenctl-dist --pattern tercenctl-darwin-arm64
```

Windows: the asset is `tercenctl-windows-x64.exe`. Available platforms:
linux-x64, windows-x64.exe, darwin-arm64, darwin-x64.

Or use the `install-tercenctl` skill from `tercen/skills` — it picks the right
binary for your platform, checks the download against the published checksum,
and installs it. Ask Claude Code to "install tercenctl" and it will run.

There is also a public container image, `tercen/tercenctl:<version>` on Docker
Hub, which needs no access to this repository:

```bash
docker run --rm -e TERCEN_URI -e TERCEN_USERNAME -e TERCEN_PASSWORD \
  tercen/tercenctl:0.10.0 --version
```

## Verifying a download

Each release carries `SHA256SUMS`:

```bash
curl -fL -o SHA256SUMS \
  https://github.com/tercen/tercenctl-dist/releases/latest/download/SHA256SUMS
sha256sum -c SHA256SUMS --ignore-missing
```

## How releases get here

The `Release tercenctl` workflow in `tercen/sci` builds the binaries on a
`tercenctl-v*` tag push, generates `SHA256SUMS` over the complete set,
verifies the published assets by re-downloading them, and only then marks the
release public. Releases are never created in this repository by hand, so that
what is published always matches a commit in the source repository.
