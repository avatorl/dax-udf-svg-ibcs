---
applyTo: "**/README.md"
---

# README Authoring Rules

`src/README.md` is displayed on [daxlib.org](https://daxlib.org/) alongside the library. Follow the [DAX Lib README Guidelines](https://docs.daxlib.org/contribute/readme-guidelines).

## Document Structure (mandatory order)

```
# About PowerofBI.IBCS
  <intro paragraph>
  <IBCS disclaimer paragraph>
  <link to powerofbi.org/ibcs/>
  Author: [Name](linkedin-url)

## Usage Instructions
  <how to use section — do not change unless Power BI integration steps change>

## Functions included in the package
  <one ### subsection per function, in logical grouping order>

## License
  This project is licensed under the MIT License.
```

## Function Entry Schema

Every function gets a `###` subsection. Follow this exact structure:

```markdown
### PowerofBI.IBCS.<ChartType>.<Variant>

<One or two sentences describing what the chart visualizes and what it compares.>

<img alt="image" src="https://raw.githubusercontent.com/avatorl/dax-udf-svg-ibcs/refs/heads/main/docs/images/<filename>.png" /><br>

Recommended to use in <Visual1>, <Visual2> visuals.
```

Rules:
- Heading must exactly match the DAX function name
- Description sentence must state what values are shown and what they compare (e.g., "actual year vs. previous year")
- Image `src` must use the raw GitHub URL base: `https://raw.githubusercontent.com/avatorl/dax-udf-svg-ibcs/refs/heads/main/docs/images/`
- Image must have `alt="image"` attribute
- Do not wrap images in links
- `<br>` after the image tag
- "Recommended to use in ..." line always present; list applicable Power BI visuals (Table, Matrix, Button Slicer, etc.)
- Optional: additional notes or external links after the recommended-visual line

## Media Rules

- All image URLs must be stable raw GitHub URLs (no in-package paths, no Base64 embeds)
- Do not include images that imitate DAX Lib website UI elements
- Do not wrap images in links (images must not be clickable)
- Preserve aspect ratio; prefer `width` only when specifying dimensions

## Links

- External links must be safe and trustworthy
- PBIX example files link: `https://github.com/avatorl/dax-udf-svg-ibcs/tree/main/docs/pbix`

## Forbidden

- No inline CSS overriding global styles
- No `<iframe>` elements
