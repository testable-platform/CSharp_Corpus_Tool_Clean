# MiniCover

Synthetic, clean-by-design C# project for **MiniCover**.

Package: MiniCover 3.10.0 (NuGet global tool)

Domain: citrus grove irrigation zones (GroveIrrigation)

**Not installed here**: see Notes for why, and what was checked instead.

## What a passing result looks like

MiniCover's IL-instrumented coverage run would report full statement coverage for GroveIrrigation.

## Command

```bash
minicover instrument && dotnet test && minicover report
```

## Notes

`dotnet tool install -g minicover` requires NuGet, which this sandbox's egress proxy refuses. Per the project's own build-contract doc (read from MiniCover's own `.csproj`), it additionally declares SDK 8.0/9.0/10.0 only -- the one tool setting a floor across the whole corpus, the same shape as TypeScript's madge or Java's JaCoCo -- but that floor is moot here since the package cannot be obtained at all.

## Per-family results

Boundary families this tool was exploded into, and what each one's own real invocation found (not asserted -- see `_generator/verify_live.py`):

| Family | Toolchain | Compiles | Result |
|---|---|---|---|
| `net9` | net9.0 (manual csc, SDK 10.0.112's compiler + installed 10.0.12 runtime, rollForward LatestMajor) | yes | NOT_INSTALLED |

Per-family notes:

**net9**: Genuinely unreachable in this sandbox -- same reason as the single-version baseline, unaffected by target framework (see this file's own 'Notes' section above).

This repo carries only the `net9` family.
