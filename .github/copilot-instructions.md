# PowerofBI.IBCS - AI Agent Guidelines

DAX library for generating IBCS-compliant SVG visualizations in Power BI. All functions return `data:image/svg+xml` URIs that embed in core Power BI visuals (table, matrix, button slicer).

> Detailed authoring rules are in scoped instruction files under `.github/instructions/`.

## Architecture

### File Organization
```
.
├── .github/
│   ├── copilot-instructions.md      # AI agent guidelines (this file)
│   └── workflows/
│       └── publish-package.yml       # Workflow to publish library version to daxlib/daxlib
├── src/
│   ├── lib/
│   │   └── functions.tmdl            # Required - All DAX UDF definitions (~2800 lines)
│   ├── icon.png                      # Optional - Library icon (PNG, max 100 KB)
│   ├── README.md                     # Optional - Library docs for daxlib.org (Markdown, max 100 KB)
│   └── manifest.daxlib               # Required - Package metadata (JSON)
├── docs/
│   ├── images/                       # Documentation images
│   └── pbix/                         # Sample Power BI files for testing
└── README.md                         # Repository info
```

- [manifest.daxlib](../src/manifest.daxlib): Package metadata (id, version, authors, description, tags, URLs)
- [functions.tmdl](../src/lib/functions.tmdl): All UDF definitions (single file, ~2800 lines)

### Chart Types
- **BarChart**: Horizontal bars (AbsoluteValues, AbsoluteVariance, RelativeVariance)
- **ColumnChart**: Vertical columns (WithAbsoluteVariance, WithWaterfall, SmallMultiple, Stacked)
- **Waterfall**: P&L structure visualizations
- **PieChart**: Percentage breakdowns

## Build and Test

### Distribution
- **Development**: This GitHub repo (may contain broken code)
- **Stable releases**: [DAX Lib](https://daxlib.org/package/PowerofBI.IBCS/)
- **Documentation**: [powerofbi.org/ibcs](https://powerofbi.org/ibcs)

### Version Management
Update `version` in [manifest.daxlib](../src/manifest.daxlib) before every release. See `manifest.instructions.md` for field details.

### Publishing to DAX Lib
This repo uses the `publish-package.yml` GitHub Actions workflow to publish new versions:
1. Update version in [manifest.daxlib](../src/manifest.daxlib)
2. Navigate to Actions → `publish-package` → Run workflow
3. The workflow creates a branch on the `daxlib/daxlib` fork with the library version
4. Open a pull request from that branch to `daxlib/daxlib`
5. DAX Lib maintainers review and merge; the library is then published on [daxlib.org](https://daxlib.org/)

If changes are requested during review, apply fixes in this repo and re-run the workflow — the PR updates automatically.

### Testing
Sample PBIX files: [docs/pbix/](../docs/pbix/) directory

### Power BI Integration
1. Create measure calling UDF with all parameters
2. Set measure data category to "Image URL"
3. Add to visual (table column, matrix value, button slicer image, etc.)
4. Adjust image height/width in Format pane

## Security

- All chart generation is client-side (DAX evaluation in Power BI)
- SVG escaping: Handle special chars in data labels (`&`, `<`, `>`, `"`, `'`)
- No external dependencies or API calls
