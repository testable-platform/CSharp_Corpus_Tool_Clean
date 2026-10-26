# altcover

Synthetic, clean-by-design C# project for **altcover**.

Package: AltCover (NuGet global tool / MSBuild package)

Domain: cold storage pallet ledger (ColdStorageLedger)

**Not installed here**: see Notes for why, and what was checked instead.

## What a passing result looks like

AltCover's IL-weaving instrumentation of ColdStorageLedger would report full statement/branch coverage from a real xUnit run.

## Command

```bash
dotnet test /p:AltCover=true
```

## Notes

AltCover ships only as a NuGet package (`altcover` global tool or `altcover.api`); this sandbox's egress proxy refuses `api.nuget.org` (`connect_rejected`/403, measured directly with `dotnet restore`), so nothing with a `PackageReference` resolves. The project's own `csharp-repos-build-contract.md` documents the identical block: 'Nothing with a PackageReference can restore.' The source still compiles clean with `dotnet build` against zero external packages.

## Per-family results

Boundary families this tool was exploded into, and what each one's own real invocation found (not asserted -- see `_generator/verify_live.py`):

| Family | Toolchain | Compiles | Result |
|---|---|---|---|
| `net10` | net10.0 (dotnet-sdk-10.0, native) | yes | NOT_INSTALLED |

Per-family notes:

**net10**: Genuinely unreachable in this sandbox -- same reason as the single-version baseline, unaffected by target framework (see this file's own 'Notes' section above).

This repo carries only the `net10` family.
