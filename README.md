# sprint7-final-project
Análisis de datos de ConnectaTel: limpieza, exploración, segmentación de clientes, detección de outliers y recomendaciones comerciales con Python.

## 1. Descripción del proyecto

Este proyecto analiza el comportamiento de los clientes de **ConnectaTel**, una empresa de telecomunicaciones con operaciones en México y Colombia.

El objetivo es comprender los patrones de uso de llamadas y mensajes, identificar valores atípicos y segmentar a los clientes según sus características demográficas y su nivel de consumo.

A partir de los resultados, se plantean recomendaciones comerciales para optimizar la oferta de planes, identificar oportunidades de activación y mejorar la experiencia del cliente.

## 2. Objetivos del análisis

- Explorar y limpiar datos provenientes de diferentes fuentes.
- Identificar valores faltantes, sentinels, fechas fuera de rango e inconsistencias.
- Calcular estadísticas descriptivas del comportamiento de los clientes.
- Visualizar las distribuciones de edad y consumo mediante histogramas.
- Detectar valores atípicos mediante el rango intercuartílico (IQR).
- Segmentar clientes por edad y nivel de uso.
- Formular conclusiones y recomendaciones comerciales basadas en los datos.

## 3. Datasets utilizados

El análisis utiliza tres archivos CSV:

| Dataset | Descripción |
|---|---|
| `plans.csv` | Catálogo de planes, precios, minutos y mensajes incluidos, gigabytes y tarifas adicionales. |
| `users_latam.csv` | Información de clientes: identificador, edad, ciudad, fecha de registro, plan contratado y fecha de cancelación. |
| `usage.csv` | Registros de actividad de los clientes: llamadas, mensajes, fechas, duración y longitud. |

Los tres archivos se complementan para relacionar las características de los clientes con su comportamiento de uso.

## 4. Herramientas y tecnologías

- **Python:** procesamiento y análisis de datos.
- **Pandas:** exploración, limpieza, transformación y agregación.
- **NumPy:** operaciones numéricas y segmentación de clientes.
- **Matplotlib:** visualización de datos.
- **Seaborn:** histogramas y boxplots.
- **Jupyter Notebook / Google Colab:** ejecución y documentación del análisis.
- **GitHub:** almacenamiento y publicación del proyecto.

## 5. Etapas del análisis

### Paso 1. Carga y exploración

Se cargaron los tres datasets y se revisaron sus primeras filas, dimensiones, columnas, tipos de datos y valores no nulos.

### Paso 2. Identificación de problemas de calidad

Se analizaron valores faltantes, sentinels, categorías desconocidas y fechas fuera del periodo establecido.

Entre los hallazgos se identificaron:

- Un valor centinela `-999` en la columna `age`.
- 469 ciudades nulas y 96 registros con `?` en la columna `city`.
- 40 fechas de registro de 2026, fuera del periodo de análisis hasta 2024.
- Valores nulos en `date`, `duration` y `length` dentro de `usage`.

### Paso 3. Limpieza básica

Se reemplazó el sentinel de edad por la mediana calculada a partir de las edades válidas, se estandarizaron los valores `?` de `city` como faltantes y se marcaron como nulas las fechas de registro posteriores a 2024.

También se comprobó que los valores nulos de `duration` y `length` estaban asociados principalmente al tipo de actividad: llamadas y mensajes. Por ello, se conservaron como nulos cuando la variable no aplicaba.

### Paso 4. Estadísticas descriptivas

Se agregaron los registros de actividad por usuario para calcular:

- Cantidad de mensajes.
- Cantidad de llamadas.
- Minutos acumulados de llamadas.

Estas métricas se combinaron con la información de los clientes para analizar sus características demográficas y contractuales.

### Paso 5. Visualización y detección de outliers

Se crearon histogramas para estudiar las distribuciones de edad y consumo, además de boxplots para identificar posibles valores atípicos.

Mediante el método IQR se encontraron:

- **Edad:** 0 posibles outliers.
- **Mensajes:** 46 posibles outliers.
- **Llamadas:** 30 posibles outliers.
- **Minutos de llamadas:** 109 posibles outliers.

Los valores extremos se conservaron provisionalmente porque pueden representar comportamientos reales y no necesariamente errores de registro.

### Paso 6. Segmentación de clientes

Se crearon dos variables para clasificar a los usuarios:

**Por nivel de uso:**
- Bajo uso.
- Uso medio.
- Alto uso.

La clasificación se realizó según las cantidades de llamadas y mensajes registradas por usuario.

**Por edad:**
- Joven: menor de 30 años.
- Adulto: de 30 a 59 años.
- Adulto Mayor: 60 años o más.

Se utilizaron gráficos de barras para visualizar la distribución de los clientes en cada segmento.

### Paso 7. Insights ejecutivos y recomendaciones

Se sintetizaron los problemas de calidad, los patrones de consumo y los segmentos identificados.

Las oportunidades comerciales propuestas incluyen evaluar campañas de activación para clientes de bajo uso, analizar beneficios adicionales para clientes de alto uso y comparar las necesidades de los grupos de edad y planes contratados.

## 6. Estructura del repositorio

```text
sprint7-final-project/
├── README.md
├── S7 Version-Estudiante-Project-ConnectaTel.ipynb
└── datasets/
    ├── plans.csv
    ├── users_latam.csv
    └── usage.csv
```

La carpeta `datasets/` es necesaria si se desea ejecutar el notebook con las rutas relativas propuestas. Los archivos CSV solo deben publicarse si existe autorización para compartirlos.

## 7. Cómo ejecutar el notebook

### Opción A. Google Colab

1. Abre [Google Colab](https://colab.research.google.com/).
2. Selecciona **Archivo → Abrir notebook → GitHub**.
3. Introduce la URL del repositorio.
4. Busca y abre `S7 Version-Estudiante-Project-ConnectaTel.ipynb`.
5. Carga los tres archivos CSV en la ubicación esperada por el notebook.
6. Ejecuta las celdas en orden, desde la carga de datos hasta las conclusiones.

Si utilizas Google Colab y los archivos están dentro de `/content/datasets/`, las instrucciones de carga pueden ser:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

plans = pd.read_csv('/content/datasets/plans.csv')
users = pd.read_csv('/content/datasets/users_latam.csv')
usage = pd.read_csv('/content/datasets/usage.csv')
```

Adapta las rutas a la ubicación real de los archivos en tu entorno.

### Opción B. Ejecución local

1. Instala Python y Jupyter Notebook.
2. Descarga o clona el repositorio.
3. Coloca los tres CSV dentro de la carpeta `datasets/`.
4. Instala las dependencias necesarias:

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

5. Abre Jupyter Notebook:

```bash
jupyter notebook
```

6. Abre `S7 Version-Estudiante-Project-ConnectaTel.ipynb`.
7. Ejecuta las celdas secuencialmente.

## 8. Guía de reproducción

Para reproducir el análisis:

1. Utiliza los datasets originales del proyecto.
2. Mantén los nombres de archivo y las columnas esperadas por el notebook.
3. Verifica las rutas de carga de los CSV antes de ejecutar el análisis.
4. Ejecuta todas las celdas en orden para asegurar que las variables y transformaciones estén disponibles.
5. Comprueba los resultados de limpieza, estadísticas descriptivas, outliers y segmentación.
6. Documenta cualquier cambio en las reglas de limpieza o en las rutas de los archivos.
7. Ejecuta el notebook completo desde el principio para verificar que los resultados se reproduzcan correctamente.

## 9. Conclusiones

El análisis permitió identificar problemas de calidad de datos, describir las distribuciones de consumo y construir segmentos de clientes por edad y nivel de uso.

La detección de valores atípicos permitió reconocer usuarios con consumos extremos que requieren revisión, sin asumir que representan errores.

Los resultados ofrecen una base inicial para diseñar ofertas diferenciadas y mejorar la experiencia del cliente. Como trabajo adicional, se recomienda profundizar en la relación entre consumo, plan contratado, ingresos y cancelaciones para priorizar las estrategias con mayor impacto comercial.

## 10. Autoría

Proyecto desarrollado como parte del Sprint 7 de formación en análisis de datos, Estudiante Santiago Hoyos.

**Tecnologías:** Python, Pandas, NumPy, Matplotlib, Seaborn, Jupyter Notebook y GitHub.
