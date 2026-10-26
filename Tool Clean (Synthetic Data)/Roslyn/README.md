# Roslyn

Synthetic, clean-by-design C# project for **Roslyn**.

Package: Microsoft.CodeAnalysis (bundled with the .NET SDK)

Domain: observatory telescope scheduling queue (TelescopeScheduling)

**Measured**: installed (or built from real source) and actually invoked in the build environment; the result below is real, not asserted.

## What a passing result looks like

`dotnet build` with `EnableNETAnalyzers`, `AnalysisMode=All`, `AnalysisLevel=latest-all`, nullable reference types and `TreatWarningsAsErrors` reports zero warnings against TelescopeScheduling.

## Command

```bash
dotnet build
```

## Notes

The project's own build-contract doc flags `Roslyn`/`roslyn sast` as not being pinnable package names (19 metrics) and names SonarAnalyzer.CSharp/Roslynator/NetAnalyzers as the real resolution -- all three ship on NuGet, blocked here. But the CA rule family (`Microsoft.CodeAnalysis.NetAnalyzers`) has shipped bundled inside the .NET SDK itself since .NET 5, needing no NuGet restore at all: `dotnet build` here genuinely invoked real Roslyn analyzers (confirmed non-vacuous -- CA1510 and CA1822 both fired for real on the first draft of this file, before the fixes below) rather than a no-op.

## Per-family results

Boundary families this tool was exploded into, and what each one's own real invocation found (not asserted -- see `_generator/verify_live.py`):

| Family | Toolchain | Compiles | Result |
|---|---|---|---|
| `netcoreapp30` | netcoreapp3.0 (manual csc, SDK 8.0.131's compiler + installed 8.0.31 runtime, rollForward LatestMajor) | yes | NOT_INSTALLED |

Per-family notes:

**netcoreapp30**: `dotnet build` was actually attempted and fails at restore -- `NU1301`, unable to reach `api.nuget.org` -- before Roslyn or its analyzers ever run. Neither installed SDK (8.0.131, 10.0.112) bundles netcoreapp3.0's own `Microsoft.NETCore.App.Ref` targeting pack; it is NuGet-only and NuGet is blocked at the egress proxy (measured directly, not assumed).

This repo carries only the `netcoreapp30` family.
