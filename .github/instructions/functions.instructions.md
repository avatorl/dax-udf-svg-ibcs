---
applyTo: "**/functions.tmdl"
---

# DAX Function Authoring Rules

## Naming

- Function namespace: `'PowerofBI.IBCS.<ChartType>.<Variant>'` — PascalCase segments separated by dots
- No DAX reserved keywords in any name segment (`FILTER`, `DATE`, `MEASURE`, `FUNCTION`, `DEFINE`)
- No `Dax.` or `DaxLib.` as a package name prefix

## Parameter Conventions

Use these standard parameter names consistently:

| Category | Parameters |
|---|---|
| Values | `valueMain`, `valueAC`, `valuePY`, `valueFC`, `valueBase` |
| Image sizing | `imageWidth`, `imageHeight`, `imageRightPad` (0 = use default) |
| Booleans | `isTotalRow`, `chartInTotalRow`, `showPieChart` |
| Labels | `dataLabel`, `periodLabel`, `axisLabel` |
| Type enums | `chartType`, `varianceType`, `baseType` (string values like `"AC"`, `"PY"`) |
| Business logic | `businessImpact` (1 = positive is good, −1 = positive is bad) |

## Function Body: Mandatory 4-Section Structure

Every function must follow this exact order with section header comments:

```dax
function 'PowerofBI.IBCS.ChartType.Variant[.Subvariant]' = (params) =>
    //=================================================================================================
    // Project: PowerofBI.IBCS: IBCS-guided data visualizations in your Power BI reports
    // Project website: https://www.powerofbi.org/ibcs
    // Author: Andrzej Leszkiewicz — IBCS® Certified Analyst
    // LinkedIn: https://www.linkedin.com/in/avatorl/
    // The visualization design adheres to IBCS recommendations,
    //      but this function is NOT produced, certified, authorized, or endorsed by IBCS®
    // License: MIT License (free and permissive)
    //=================================================================================================

    //=================================================================================================
    // CONFIGURATION: chart formatting and internal constants
    //=================================================================================================
    VAR _DEBUG = 0
    // ... colors, sizes, defaults

    //=================================================================================================
    // CALCULATIONS: Convert data values into pixel dimensions, apply logic for colors and labels
    //=================================================================================================
    // ... scaling logic

    //=================================================================================================
    // SVG GENERATION: Build all SVG components
    //=================================================================================================
    VAR _SVG_Header = "data:image/svg+xml;utf8,"
    VAR _SVG_Open = "<svg xmlns='http://www.w3.org/2000/svg' width='" & _SVG_Width & "' >"
    // ... SVG element vars
    VAR _SVG_Close = "</svg>"

    VAR _Result = _SVG_Header & _SVG_Open & _SVG_Body & _SVG_Close
    RETURN _Result
```

## Variable Naming

- Colors: `_Color<Name>` — e.g., `_ColorMain`, `_ColorRed`, `_ColorGreen`
- Layout/SVG: `_SVG_<Component>` — e.g., `_SVG_Width`, `_SVG_LeftPadding`, `_SVG_Header`
- Calculations: `_PascalCase` prefix with underscore — e.g., `_WidthMain`, `_Scale`, `_Rank`
- Constants: descriptive uppercase words — e.g., `_DEBUG`, `_SVG_Width_Default`

## IBCS Color Palette — never change these hex values

```dax
VAR _ColorMain    = "#404040"  // Black  — actuals (AC)
VAR _ColorGrey    = "#C6C6C6"  // Grey   — previous year (PY)
VAR _ColorRed     = "#E24B20"  // Red    — negative variance
VAR _ColorGreen   = "#08787D"  // Green  — positive variance
VAR _ColorOutline = "#FFFFFF"  // White  — outlines
```

Do not introduce arbitrary hex colors outside this palette.

## Critical Rules

1. **Never hardcode variance colors.** Always derive from `businessImpact` parameter:
   ```dax
   VAR _barColor = IF ( valueMain * businessImpact > 0, _ColorGreen, _ColorRed )
   ```
   `businessImpact = 1` → positive is good (sales); `businessImpact = -1` → positive is bad (costs).

2. **`VAR _DEBUG = 0`** must appear in the CONFIGURATION section of every function.

3. **Font pt → px conversion** — never use raw pt values in SVG:
   ```dax
   VAR _FontSizePt = 14
   VAR _Em = _FontSizePt * 4 / 3
   ```

4. **Optional image parameters default to 0.** Resolve inside the function:
   ```dax
   VAR _SVG_Width = IF ( imageWidth > 0, imageWidth, _SVG_Width_Default )
   VAR _SVG_RightPadding = IF ( imageRightPad > 0, imageRightPad, 190 )
   ```

5. **No `CreateOrReplace`** keyword anywhere in the TMDL file.

6. **Escape SVG data labels**: replace `&` → `&amp;`, `<` → `&lt;`, `>` → `&gt;`, `"` → `&quot;`

## DAXLIB Annotations — end of every function

```dax
annotation DAXLIB_PackageId = __PLACEHOLDER_PACKAGE_ID__
annotation DAXLIB_PackageVersion = __PLACEHOLDER_PACKAGE_VERSION__
```

## Documentation — mandatory JSDoc-style before every function

```dax
/// Multi-line description of chart purpose and visual design.
/// @param {scalar} valueMain - actual value: [AC]
/// @param {boolean} isTotalRow - total row indicator: NOT ( ISINSCOPE ( 'Category'[Category] ) )
/// @returns SVG image (data:image/svg+xml URI for embedding in table cells)
function 'PowerofBI.IBCS.ChartType.Variant' =
```

Every `@param` entry must include: **type**, **description**, and an **example DAX expression**.


Helps users create and manage User-Defined Functions (UDFs) in their codebase. Assist with writing UDFs, optimizing them for performance, and integrating them into existing projects. Provide guidance on best practices for UDF development and troubleshoot any issues that arise during implementation.

When asked to install functions from TMDL file to the model, follow these steps (unless there are best practices or other instructions that should be followed instead):

Connect to Model:

Use mcp_powerbi-model_connection_operations


From TMDL: Copy only the code after the => operator
Exclude the function signature line: function 'name' = (

Update Functions

Use mcp_powerbi-model_function_operations with Update operation
Provide: name, description, expression (DAX only)

Parameter Syntax Rule

✅ Correct: (param: SCALAR VAL, ...)
❌ Wrong: (param as SCALAR VAL, ...)

Batch Updates

Group multiple functions in one definitions array
