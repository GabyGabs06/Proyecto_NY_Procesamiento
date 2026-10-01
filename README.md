# Ventanas de riesgo en Nueva York

**¿Dónde y cuándo conviene reforzar el patrullaje, el control de tránsito y la respuesta de emergencia?**

Nueva York registró en 2025 el año más seguro de su historia en materia de tránsito, pero el riesgo no se reparte por igual: cambia según el borough, la hora, el día de la semana y el clima. Este proyecto construye un **índice de urgencia** que ordena las combinaciones de esos factores para que el gobierno del estado asigne sus recursos operativos donde más se necesitan, en lugar de repartirlos de forma uniforme.

Procesamos millones de registros públicos con **Apache Spark** y seguimos la metodología **CRISP-DM**.

---

## El enfoque

Cada **ventana de riesgo** es una combinación de:

| Dimensión | Valores |
|---|---|
| Zona | Los 5 boroughs |
| Franja horaria | 4 franjas de 6 horas |
| Día | Lunes a domingo |
| Clima | Despejado, nublado, lluvia, nieve |

Para cada ventana se calcula un puntaje de urgencia con dos componentes:

- **Vial:** frecuencia de choques y proporción de choques con heridos o fallecidos.
- **Seguridad:** denuncias por delitos graves.

Las frecuencias se ajustan por las **horas realmente observadas** de cada condición y por la **población** de cada borough, para que una zona grande no parezca más peligrosa solo por tener más gente. Los arrestos se usan como referencia de actividad policial (para no confundir más presencia policial con más delincuencia) y la pobreza como contexto para ver si las zonas más urgentes son también las más vulnerables.

## Datos

Todo es público. Los datos crudos no se incluyen en el repositorio por su tamaño; las instrucciones de descarga están en [`data/README.md`](data/README.md).

| Fuente | Qué aporta | Enlace |
|---|---|---|
| Motor Vehicle Collisions – Crashes | Choques, heridos y fallecidos | [NYC Open Data](https://data.cityofnewyork.us/Public-Safety/Motor-Vehicle-Collisions-Crashes/h9gi-nx95/about_data) |
| NYPD Complaint Data Historic | Denuncias con fecha, hora y lugar | [NYC Open Data](https://data.cityofnewyork.us/Public-Safety/NYPD-Complaint-Data-Historic/qgea-i56i/about_data) |
| NYPD Arrests Data (Historic) | Actividad policial por día y zona | [NYC Open Data](https://data.cityofnewyork.us/Public-Safety/NYPD-Arrests-Data-Historic-/8h9b-rp9u/about_data) |
| NYCgov Poverty Measure (2018) | Pobreza por borough | [NYC Open Data](https://data.cityofnewyork.us/City-Government/NYCgov-Poverty-Measure-Data-2018-/cts7-vksw/about_data) |
| Open-Meteo Historical API | Clima horario por borough | [Open-Meteo](https://open-meteo.com/en/docs/historical-weather-api) |
| Población por borough | Normalización por habitantes | _[completar enlace y año del scraping]_ |

## Hallazgos

_En construcción. Aquí irán las ventanas de mayor urgencia, los patrones por hora y clima, y las recomendaciones para el gobierno._

## Estructura del repositorio

```
├── notebooks/
│   └── Proyecto.ipynb        # Análisis completo en PySpark
├── docs/                     # Informes y presentaciones (PDF)
├── figures/                  # Gráficas generadas por el análisis
├── data/
│   └── README.md             # Cómo obtener los datos
├── requirements.txt
└── README.md
```

## Cómo reproducirlo

```bash
# 1. Instalar dependencias
pip install -r requirements.txt

# 2. Descargar los datos (ver data/README.md) y ubicarlos en data/raw/

# 3. Ejecutar el cuaderno completo
jupyter notebook notebooks/Proyecto.ipynb
```

El análisis corre sobre **Apache Spark 4.0.4** (PySpark) en máquinas virtuales con servidor Jupyter. _[completar: nodos, workers, memoria y si se usa HDFS]_

## Hoja de ruta

- [x] Entendimiento del negocio y de los datos
- [x] Exploración y reporte de calidad de datos
- [ ] Limpieza y transformación completas
- [ ] Respuesta a las preguntas de negocio
- [ ] Modelado con Spark MLlib (técnica supervisada y no supervisada)
- [ ] Evaluación de modelos y recomendaciones finales

## Equipo

Gabriela Alejandra Muñoz Tovar · Mónica María Castro Benítez · Lorenzo Ramírez Calderón · Luis Alexander Pedraza Béltran

<sub>Proyecto desarrollado en el curso Procesamiento de Alto Volumen de Datos, Pontificia Universidad Javeriana.</sub>
