# tercenctl distribution

Release artefacts for `tercenctl`, the Tercen command line tool. The source
lives in the private `tercen/sci` repository; this repository carries nothing
but the built binaries, so that people who should have the tool can be given
access to it without being given access to the source.

## Getting it

Use the `install-tercenctl` skill from `tercen/skills` — it picks the right
binary for your platform, checks the download against the published checksum,
and installs it. Ask Claude Code to "install tercenctl" and it will run.

By hand, if you prefer:

```bash
gh release download tercenctl-v0.10.0 --repo tercen/tercenctl-dist \
  --pattern tercenctl-linux-x64 --output ~/.local/bin/tercenctl
chmod +x ~/.local/bin/tercenctl
tercenctl --version
```

Windows: the same command with `--pattern tercenctl-windows-x64.exe`.

There is also a public container image, `tercen/tercenctl:<version>` on Docker
Hub, which needs no access to this repository:

```bash
docker run --rm -e TERCEN_URI -e TERCEN_USERNAME -e TERCEN_PASSWORD \
  tercen/tercenctl:0.10.0 --version
```

## Verifying a download

Each release carries `SHA256SUMS`:

```bash
gh release download <tag> --repo tercen/tercenctl-dist --pattern SHA256SUMS
sha256sum -c SHA256SUMS --ignore-missing
```

## Access

Read access is granted per person. Anyone in the `tercen` organisation already
has it; everyone else is added as an outside collaborator. Access is revoked by
removing that collaborator — nothing else needs to change.

## How releases get here

The `Release tercenctl` workflow in `tercen/sci` builds the binaries and
publishes them here. Releases are never created in this repository by hand, so
that what is published always matches a commit in the source repository.
