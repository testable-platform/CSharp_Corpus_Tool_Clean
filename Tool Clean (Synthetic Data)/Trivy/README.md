# Trivy

Synthetic, clean-by-design C# project for **Trivy**.

Package: github.com/aquasecurity/trivy (Go binary / GitHub release)

Domain: shipping container package manifest (ContainerManifestScan)

**Not installed here**: see Notes for why, and what was checked instead.

## What a passing result looks like

A Trivy filesystem scan of ContainerManifestScan's declared packages would report zero known-vulnerable dependencies.

## Command

```bash
trivy fs .
```

## Notes

Trivy ships as a GitHub Release binary or via its own apt repository at `aquasecurity.github.io`; both return 403 at this sandbox's egress proxy (measured directly), and `go install` is blocked the same way it was in the sibling TypeScript and Java corpora (`proxy.golang.org` not in the allowlist). No package for it exists in Ubuntu's own apt archive.

## Per-family results

Boundary families this tool was exploded into, and what each one's own real invocation found (not asserted -- see `_generator/verify_live.py`):

| Family | Toolchain | Compiles | Result |
|---|---|---|---|
| `netcoreapp30` | netcoreapp3.0 (manual csc, SDK 8.0.131's compiler + installed 8.0.31 runtime, rollForward LatestMajor) | yes | NOT_INSTALLED |

Per-family notes:

**netcoreapp30**: Genuinely unreachable in this sandbox -- same reason as the single-version baseline, unaffected by target framework (see this file's own 'Notes' section above).

This repo carries only the `netcoreapp30` family.
