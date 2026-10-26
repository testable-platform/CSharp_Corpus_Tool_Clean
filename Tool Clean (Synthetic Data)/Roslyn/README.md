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
| `net9` | net9.0 (manual csc, SDK 10.0.112's compiler + installed 10.0.12 runtime, rollForward LatestMajor) | yes | NOT_INSTALLED |

Per-family notes:

**net9**: Same failure mode as netcoreapp3.0, one family later: `dotnet build` under SDK 10.0.112 reaches restore and fails with the identical `NU1301` -- net9.0's own targeting pack is NuGet-only too. The manual `csc` compile this corpus uses elsewhere for net9.0 bypasses MSBuild entirely, which is exactly why it cannot carry the MSBuild-integrated NetAnalyzers pipeline with it.

This repo carries only the `net9` family.
