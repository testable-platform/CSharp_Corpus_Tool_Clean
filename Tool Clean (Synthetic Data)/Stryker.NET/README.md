# Stryker.NET

Synthetic, clean-by-design C# project for **Stryker.NET**.

Package: dotnet-stryker (NuGet global tool)

Domain: tea plantation harvest grading (HarvestGrading)

**Not installed here**: see Notes for why, and what was checked instead.

## What a passing result looks like

Stryker.NET's real mutation-testing run against HarvestGrading would kill every mutant its operators can generate -- 100% mutation score.

## Command

```bash
dotnet stryker
```

## Notes

`dotnet tool install -g dotnet-stryker` requires NuGet, which this sandbox's egress proxy refuses; Stryker.NET also needs a restorable test project (xUnit/NUnit/MSTest), themselves NuGet-only and equally unreachable. The project's own build-contract doc separately flags Stryker.NET as a category error for the Data-Flow-coverage metrics it is declared primary for (a mutation tester computes no def-use chains) -- a defect in the roster independent of this sandbox's network block.

## Per-family results

Boundary families this tool was exploded into, and what each one's own real invocation found (not asserted -- see `_generator/verify_live.py`):

| Family | Toolchain | Compiles | Result |
|---|---|---|---|
| `netcoreapp30` | netcoreapp3.0 (manual csc, SDK 8.0.131's compiler + installed 8.0.31 runtime, rollForward LatestMajor) | yes | NOT_INSTALLED |

Per-family notes:

**netcoreapp30**: Genuinely unreachable in this sandbox -- same reason as the single-version baseline, unaffected by target framework (see this file's own 'Notes' section above).

This repo carries only the `netcoreapp30` family.
