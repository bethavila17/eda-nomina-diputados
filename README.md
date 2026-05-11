# Trabajo Práctico Final — Pipeline Integral de Ciencia de Datos

**Análisis, Modelado y Evaluación Aplicados sobre la Nómina de la Cámara de Diputados — Paraguay 2025**

| Campo | Detalle |
|---|---|
| **Materia** | Introducción a la Ciencia de Datos |
| **Autores** | Bethania Avila · Alfredo Coronel |
| **Fecha** | Mayo 2026 |
| **Dataset** | Nómina Pública 2025 — Cámara de Diputados (Ministerio de Hacienda PY) |

---

## Estructura del repositorio

```
tp_final/
├── data/
│   ├── README.md              # Instrucciones para obtener los datos
│   └── Nomina 2025/           # CSVs mensuales (no incluidos en el repo por tamaño)
│       ├── nomina-2025-01/nomina_2025-01.csv
│       ├── ...
│       └── nomina-2025-13/nomina_2025-13.csv
├── notebooks/
│   └── TP_Final_Pipeline_Ciencia_Datos.ipynb   # Notebook principal
├── reports/
│   └── TP_Final_Pipeline_Ciencia_Datos.pdf     # Informe PDF (generado con nbconvert)
├── requirements.txt           # Dependencias Python
└── README.md                  # Este archivo
```

---

## Pipeline — 5 Etapas

| Etapa | Puntaje | Descripción |
|---|---|---|
| **ETAPA 1** | 25 pts | Carga de 13 CSV, diagnóstico de nulos/duplicados, limpieza y normalización |
| **ETAPA 2** | 20 pts | EDA: distribución salarial, brecha de género, evolución mensual, Gini, correlaciones |
| **ETAPA 3** | 25 pts | Clasificación supervisada: predecir si un funcionario es de alto ingreso (RF ROC-AUC=0.93) |
| **ETAPA 4** | 15 pts | Regresión supervisada: predecir `montoDevengado` (RF R²=0.87) |
| **ETAPA 5** | 15 pts | Clustering: Antigüedad vs Salario (K-Means+centroides) y perfil de objetos de gasto (K-Means+PCA) |

---

## Instalación y ejecución

### 1. Instalar dependencias

```bash
pip install -r requirements.txt
```

### 2. Configurar datos

Descargar los 13 archivos CSV desde el Portal de Datos Abiertos del Ministerio de Hacienda:
- URL: https://datos.hacienda.gov.py/
- Colocar en la estructura indicada en `data/README.md`
- Actualizar `BASE_PATH` en el notebook si la ruta difiere

### 3. Ejecutar el notebook

```bash
# Opción A — con Jupyter Notebook
jupyter notebook notebooks/TP_Final_Pipeline_Ciencia_Datos.ipynb

# Opción B — ejecutar todo automáticamente
jupyter nbconvert --to notebook --execute --inplace notebooks/TP_Final_Pipeline_Ciencia_Datos.ipynb

# Opción C — generar PDF directamente
jupyter nbconvert --to pdf notebooks/TP_Final_Pipeline_Ciencia_Datos.ipynb
```

---

## Preguntas orientadoras respondidas

1. **¿Cómo se distribuye el gasto salarial?**  
   El Gini ≈ 0.55 indica desigualdad moderada-alta. El 10% mejor pago concentra ~40% de la masa salarial.

2. **¿Existe brecha salarial por sexo?**  
   Sí, ~10–15% en mediana anual a favor de varones, explicada por distribución desigual de cargos.

3. **¿Es posible predecir quién es alto ingreso?**  
   Sí. Random Forest logra ROC-AUC=0.93. El cargo y el tipo de personal son los predictores dominantes.

4. **¿Cuánto devengará un funcionario?**  
   Random Forest logra R²=0.87. El `codigoObjetoGasto` y el cargo explican ~90% de la varianza.

5. **¿Qué segmentos existen?**  
   - **Por antigüedad/salario (K=4)**: veteranos mal pagados (franja crítica), directivos veteranos, nuevos bien pagados, contratados.
   - **Por objetos de gasto (K=5)**: técnicos, asesores, diputados (dietas), contratados, directivos.

---

## Hallazgos clave

| Hallazgo | Detalle |
|---|---|
| Pago máximo | 507.6M Gs. en un único registro (Director General, mes 7) |
| Franja crítica | Técnicos con 8+ años y salario en Q1 |
| Anomalías P95 | Bonificaciones extraordinarias en julio y diciembre |
| Corte 13 | 3,765 registros duplicados eliminados en limpieza |

---

## Tecnologías utilizadas

- **Python 3.13** · pandas · numpy · matplotlib · seaborn
- **scikit-learn** (Logistic Regression, Random Forest, K-Means, PCA, StandardScaler)
- **Jupyter Notebook** · nbconvert
