# PowerofBI.IBCS

DAX User-Defined Functions (UDFs) for Embedding IBCS-guided SVG Visualizations into Core Visuals

About International Business Communication Standards (IBCS):

https://www.powerofbi.org/international-business-communication-standards/

https://www.powerofbi.org/category/data-visualization/ibcs/

https://www.ibcs.com/

## Usage Instructions

These UDFs generate charts that can be embedded into Power BI core visuals such as table, matrix, button slicer, or new card (depending on the chart type).  

The functions generate SVG code. Change the measure's data category to "Image URL" to ensure Power BI renders SVG images.
<img width="430" height="73" alt="image" src="https://github.com/user-attachments/assets/15b51c49-7ba1-4a28-b33b-288b1ac536ef" />


## Usage Examples

### PowerofBI.IBCS.BarChartAbsoluteValues
<img width="267" height="150" alt="image" src="https://github.com/user-attachments/assets/75cc6271-17eb-4466-bbeb-91c0641c090d" />

Use in Table, Matrix, Button List visuals

```
PowerofBI.IBCS.BarChartAbsoluteValues (
    [Sales AC],
    BLANK (),
    [Sales PY],
    "grey",
    FORMAT ( [Sales AC], "#0,," ),
    NOT ( HASONEVALUE ( 'Store'[Name] ) ),
    MAXX ( ALLSELECTED ( 'Store' ), MAX ( [Sales AC], [Sales PY] ) )
)
```

### PowerofBI.IBCS.BarChartAbsoluteVariance
<img width="378" height="161" alt="image" src="https://github.com/user-attachments/assets/8cf32b8d-bc85-48b2-bab9-93b9b09f99c5" />

Use in Table, Matrix, Button List visuals

```
PowerofBI.IBCS.BarChartAbsoluteVariance (
    [Delta PY],
    FORMAT ( [Delta PY], "#0,," ),
    NOT ( HASONEVALUE ( 'Store'[Name] ) ),
    MAXX ( ALLSELECTED ( 'Store'[Short Name] ), [Delta PY] ),
    MINX ( ALLSELECTED ( 'Store'[Short Name] ), [Delta PY] ),
    MAXX ( ALLSELECTED ( 'Store' ), MAX ( [Sales AC], [Sales PY] ) )
)
```

### PowerofBI.IBCS.BarChartRelativeVariance
<img width="290" height="150" alt="image" src="https://github.com/user-attachments/assets/c8a310e4-38d4-406d-8029-4f89bba522ad" />

Use in Table, Matrix, Button List visuals

```
PowerofBI.IBCS.BarChartRelativeVariance (
    [Delta PY%] * 100,
    FORMAT ( [Delta PY%] * 100, "+#,0;-#,0;#,0" ),
    NOT ( HASONEVALUE ( 'Store'[Name] ) )
)
```

Use in Matrix, Button List visuals

### PowerofBI.IBCS.ColumnChartWithAbsoluteVariance
<img width="1125" height="510" alt="image" src="https://github.com/user-attachments/assets/62292dfc-ce21-4daa-9bc1-1fa3ed8afab4" />

```
PowerofBI.IBCS.ColumnChartWithAbsoluteVariance (
    [MSales AC],
    [MSales PY],
    [MSales PL],
    [MSales FC],
    'Month'[Month]
)
```

## License

This project is licensed under the MIT License.
