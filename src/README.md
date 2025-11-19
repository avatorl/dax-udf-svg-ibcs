# DAX.UDF.SVG.IBCS

DAX User-Defined Function for IBCS-guided SVG visualizations

## Usage

### SVG.IBCS.AbsoluteValues
<img width="267" height="150" alt="image" src="https://github.com/user-attachments/assets/75cc6271-17eb-4466-bbeb-91c0641c090d" />

```
SVG.IBCS.AbsoluteValues (
    [Sales AC],
    BLANK (),
    [Sales PY],
    "grey",
    FORMAT ( [Sales AC], "#0,," ),
    NOT ( HASONEVALUE ( 'Store'[Name] ) ),
    MAXX ( ALLSELECTED ( 'Store' ), MAX ( [Sales AC], [Sales PY] ) )
)
```

### SVG.IBCS.AbsoluteVariance
<img width="378" height="161" alt="image" src="https://github.com/user-attachments/assets/8cf32b8d-bc85-48b2-bab9-93b9b09f99c5" />

```
SVG.IBCS.AbsoluteVariance (
    [Delta PY],
    FORMAT ( [Delta PY], "#0,," ),
    NOT ( HASONEVALUE ( 'Store'[Name] ) ),
    MAXX ( ALLSELECTED ( 'Store'[Short Name] ), [Delta PY] ),
    MINX ( ALLSELECTED ( 'Store'[Short Name] ), [Delta PY] ),
    MAXX ( ALLSELECTED ( 'Store' ), MAX ( [Sales AC], [Sales PY] ) )
)
```

##

### SVG.IBCS.RelativeVariance
<img width="290" height="150" alt="image" src="https://github.com/user-attachments/assets/c8a310e4-38d4-406d-8029-4f89bba522ad" />

```
SVG.IBCS.RelativeVariance (
    [Delta PY%] * 100,
    FORMAT ( [Delta PY%] * 100, "+#,0;-#,0;#,0" ),
    NOT ( HASONEVALUE ( 'Store'[Name] ) )
)
```

### SVG.IBCS.ColumnChart
<img width="1125" height="510" alt="image" src="https://github.com/user-attachments/assets/62292dfc-ce21-4daa-9bc1-1fa3ed8afab4" />

```
SVG.IBCS.ColumnChart ( [MSales AC], [MSales PY], [MSales PL], [MSales FC], 'Month'[Month] )
```

## Documentation

- See the `lib/functions.tmdl` file for the functions included in this library.
- See the `manifest.daxlib` file for the library metadata and configuration.

## Contributing

Contributions are welcome! Please feel free to submit issues and pull requests.

## License

This project is licensed under the MIT License.
