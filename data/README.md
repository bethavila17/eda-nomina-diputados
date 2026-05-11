# Datos — Nómina de Funcionarios Públicos 2025

## Fuente

**Portal de Datos Abiertos — Ministerio de Hacienda de Paraguay**  
URL: https://datos.hacienda.gov.py/

## Dataset utilizado

| Nombre | Valor |
|---|---|
| Dataset | Nómina de Funcionarios Públicos 2025 |
| Entidad filtrada | `003-CÁMARA DE DIPUTADOS` |
| Período | Enero–Diciembre 2025 (meses 1–12) + Corte 13 (ajuste anual) |
| Archivos | 13 CSV mensuales |
| Registros (total raw) | ~45,594 filas |
| Registros (filtrado) | ~41,829 filas (tras eliminar duplicados del corte 13) |

## Estructura de carpetas de datos

Los archivos CSV deben ubicarse en:

```
data/
└── Nomina 2025/
    ├── nomina-2025-01/
    │   └── nomina_2025-01.csv
    ├── nomina-2025-02/
    │   └── nomina_2025-02.csv
    ...
    └── nomina-2025-13/
        └── nomina_2025-13.csv
```

## Configuración de la ruta

En el notebook, actualizar la constante `BASE_PATH` si los datos están en otra ubicación:

```python
BASE_PATH = r'C:\Users\betha\eda_maestria\Nomina 2025'
# o ruta relativa:
BASE_PATH = os.path.join(os.path.dirname(os.getcwd()), 'data', 'Nomina 2025')
```

## Diccionario de datos

Ver `data/schema.json` (proporcionado por el Ministerio de Hacienda).

## Nota sobre el corte 13

El archivo `nomina_2025-13.csv` corresponde al **"corte 13"** (ajuste anual / aguinaldo proporcional). Sus registros son duplicados exactos de meses anteriores con `mesCorte=13`. Se eliminan automáticamente mediante `drop_duplicates()` en la etapa de limpieza.
