---
applyTo: "**/manifest.daxlib"
---

# Manifest Authoring Rules

`manifest.daxlib` is the package metadata file consumed by DAX Lib. Always validate against the schema.

## Schema

Always include `$schema`:
```
https://raw.githubusercontent.com/daxlib/daxlib/refs/heads/main/schemas/manifest/1.0.0/manifest.1.0.0.schema.json
```

## Required Fields

| Field | Example |
|---|---|
| `id` | `"PowerofBI.IBCS"` |
| `version` | `"0.8.1"` |
| `authors` | `"Andrzej Leszkiewicz"` |
| `description` | Concise description of what the library does |

## Optional Fields

| Field | Notes |
|---|---|
| `tags` | Comma-separated, uppercase — e.g. `"IBCS,SVG,VISUALIZATION"` |
| `releaseNotes` | Brief summary of what changed in this version |
| `projectUrl` | Public documentation URL |
| `repositoryUrl` | GitHub repository URL |
| `icon` | Path to icon PNG (max 100 KB) — e.g. `"/icon.png"` |
| `readme` | Path to README — e.g. `"/README.md"` |

## Version Bumping

- Bump `version` before every publish
- Follow semver: patch for fixes, minor for new functions, major for breaking changes
- Always update `releaseNotes` to describe what changed
