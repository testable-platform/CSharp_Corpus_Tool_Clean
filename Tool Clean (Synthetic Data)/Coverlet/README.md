# Coverlet

Synthetic, clean-by-design C# project for **Coverlet**.

Package: coverlet.collector / coverlet.msbuild (NuGet)

Domain: aviary breeding clutch record (AviaryBreedingRecord)

**Not installed here**: see Notes for why, and what was checked instead.

## What a passing result looks like

Coverlet's cross-platform coverage collector would report full statement and branch coverage from a real `dotnet test` run against AviaryBreedingRecord.

## Command

```bash
dotnet test --collect:"XPlat Code Coverage"
```

## Notes

Coverlet's collector and its VSTest data-collector plumbing are NuGet-only; `api.nuget.org` is blocked here (same measured 403 as every other NuGet-only tool in this corpus). No test framework (xUnit/NUnit/MSTest) is installable either -- all three are NuGet packages too, and Ubuntu's apt-packaged NUnit (2.6.3, Mono-era CIL assemblies) predates SDK-style .csproj entirely and cannot host a net8.0 test project. The source still compiles clean.

## Per-family results

Boundary families this tool was exploded into, and what each one's own real invocation found (not asserted -- see `_generator/verify_live.py`):

| Family | Toolchain | Compiles | Result |
|---|---|---|---|
| `netcoreapp30` | netcoreapp3.0 (manual csc, SDK 8.0.131's compiler + installed 8.0.31 runtime, rollForward LatestMajor) | yes | NOT_INSTALLED |

Per-family notes:

**netcoreapp30**: Genuinely unreachable in this sandbox -- same reason as the single-version baseline, unaffected by target framework (see this file's own 'Notes' section above).

This repo carries only the `netcoreapp30` family.
