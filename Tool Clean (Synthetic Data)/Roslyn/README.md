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
| `netfx45` | .NET Framework 4.5 (Mono 6.8.0.105 BCL profile 4.5) | yes | NOT_INSTALLED |

Per-family notes:

**netfx45**: Mono compiles and runs real .NET Framework 4.5 code, but there is no MSBuild/`dotnet build` pipeline in that path at all -- `Microsoft.CodeAnalysis.NetAnalyzers` hooks into the SDK-style build pipeline (`dotnet build`'s own analyzer targets), not into `mcs`. No SDK-style build was ever attempted for this family; it genuinely cannot happen, independent of NuGet.

This repo carries only the `netfx45` family.
