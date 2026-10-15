# sprint7-final-project
Análisis de datos de ConnectaTel: limpieza, exploración, segmentación de clientes, detección de outliers y recomendaciones comerciales con Python.


## 1. Descripción del proyecto

Este proyecto analiza el comportamiento de los clientes de **ConnectaTel**, una empresa de telecomunicaciones con operaciones en México y Colombia.

El objetivo es comprender los patrones de uso de llamadas y mensajes, identificar valores atípicos y segmentar a los clientes según sus características demográficas y su nivel de consumo.

A partir de los resultados, se plantean recomendaciones comerciales orientadas a optimizar la oferta de planes, identificar oportunidades de activación y mejorar la experiencia del cliente.

## 2. Objetivos del análisis

- Explorar y limpiar datos procedentes de diferentes fuentes.
- Identificar valores faltantes, sentinels, fechas fuera de rango e inconsistencias.
- Calcular estadísticas descriptivas del comportamiento de los clientes.
- Visualizar las distribuciones de edad y consumo.
- Detectar valores atípicos mediante el rango intercuartílico (IQR).
- Segmentar clientes por edad y nivel de uso.
- Formular conclusiones y recomendaciones comerciales basadas en los datos.
- Documentar un proceso de análisis reproducible mediante Jupyter Notebook.

## 3. Datasets utilizados

El proyecto utiliza tres archivos CSV proporcionados para la actividad:

| Dataset | Descripción |
|---|---|
| `plans.csv` | Catálogo de planes, precios, minutos y mensajes incluidos, gigabytes y tarifas adicionales. |
| `users_latam.csv` | Información de los clientes, como identificador, edad, ciudad, fecha de registro, plan contratado y fecha de cancelación. |
| `usage.csv` | Registros de actividad de los clientes, incluyendo llamadas, mensajes, fechas, duración y longitud. |

Los archivos se complementan para relacionar las características de los clientes con su comportamiento de uso.

**Disponibilidad de los datos:** los tres archivos CSV no están incluidos actualmente en este repositorio. Para ejecutar el notebook, es necesario obtenerlos desde las fuentes originales del proyecto y cargarlos en el entorno de ejecución.

## 4. Herramientas y tecnologías

- **Python:** procesamiento y análisis de datos.
- **Pandas:** exploración, limpieza, transformación y agregación.
- **NumPy:** operaciones numéricas y segmentación de clientes.
- **Matplotlib:** visualización de datos.
- **Seaborn:** histogramas y boxplots.
- **Jupyter Notebook:** desarrollo y documentación del análisis.
- **Google Colab:** alternativa para ejecutar el notebook en la nube.
- **GitHub:** almacenamiento y publicación del proyecto.

## 5. Etapas del análisis

### Paso 1. Carga y exploración

Se cargaron los tres datasets y se revisaron sus primeras filas, dimensiones, columnas, tipos de datos y valores no nulos.

### Paso 2. Identificación de problemas de calidad

Se analizaron valores faltantes, sentinels, categorías desconocidas y fechas fuera del periodo establecido.

Entre los problemas identificados se encontraron:

- Un valor centinela `-999` en la columna `age`.
- 469 valores nulos y 96 registros con `?` en la columna `city`.
- 40 fechas de registro correspondientes a 2026, fuera del periodo de análisis hasta 2024.
- Valores nulos en `date`, `duration` y `length` dentro del dataset de uso.

### Paso 3. Limpieza básica

Se reemplazó el sentinel de edad por la mediana calculada a partir de las edades válidas, se estandarizaron los valores `?` de `city` como valores faltantes y se marcaron como nulas las fechas de registro posteriores a 2024.

También se analizó la ausencia de valores en `duration` y `length` según el tipo de actividad, conservando los nulos estructurales cuando la variable no aplicaba.

### Paso 4. Estadísticas descriptivas

Se agregaron los registros de actividad por usuario para calcular:

- Cantidad de mensajes.
- Cantidad de llamadas.
- Minutos acumulados de llamadas.

Estas métricas se combinaron con la información de los clientes para estudiar sus características demográficas y contractuales.

### Paso 5. Visualización y detección de outliers

Se utilizaron histogramas para analizar las distribuciones de edad y consumo, además de boxplots para identificar posibles valores atípicos.

Mediante el método IQR se identificaron los siguientes posibles outliers:

| Variable | Posibles outliers |
|---|---:|
| Edad (`age`) | 0 |
| Mensajes (`cant_mensajes`) | 46 |
| Llamadas (`cant_llamadas`) | 30 |
| Minutos de llamadas (`cant_minutos_llamada`) | 109 |

Los valores extremos se conservaron provisionalmente, ya que pueden representar comportamientos reales y no necesariamente errores de registro.

### Paso 6. Segmentación de clientes

Se crearon dos variables de segmentación.

**Por nivel de uso:**
- **Bajo uso:** menos de 5 llamadas y menos de 5 mensajes.
- **Uso medio:** clientes que no cumplen la condición de bajo uso y tienen menos de 10 llamadas y menos de 10 mensajes.
- **Alto uso:** los demás casos.

**Por edad:**
- **Joven:** menor de 30 años.
- **Adulto:** de 30 a 59 años.
- **Adulto Mayor:** 60 años o más.

Se generaron gráficos de barras para visualizar la distribución de los clientes entre los segmentos.

### Paso 7. Insights ejecutivos y recomendaciones

Se resumieron los problemas de calidad, los patrones de consumo y los segmentos identificados.

Las oportunidades comerciales propuestas incluyen evaluar campañas de activación para clientes de bajo uso, investigar necesidades de clientes de alto uso y comparar el comportamiento de los usuarios según su edad y plan contratado.

Estas recomendaciones constituyen oportunidades para investigar; su impacto comercial debe validarse con indicadores adicionales, como ingresos, permanencia y cancelaciones.

## 6. Estructura del repositorio

Actualmente, el repositorio contiene los siguientes archivos:

```text
sprint7-final-project/
├── README.md
└── S7 Version-Estudiante-Project-ConnectaTel.ipynb
```

- **`README.md`**: documentación del proyecto, objetivos, datasets, metodología e instrucciones de reproducción.
- **`S7 Version-Estudiante-Project-ConnectaTel.ipynb`**: notebook con el proceso de exploración, limpieza, análisis estadístico, visualización, detección de valores atípicos y segmentación.

Los archivos CSV no están incluidos actualmente en el repositorio. Deben obtenerse por separado desde las fuentes originales del proyecto.

## 7. Cómo ejecutar el notebook

### Opción A. Google Colab

1. Descarga los tres archivos CSV desde los enlaces proporcionados en las instrucciones del proyecto.
2. Abre [Google Colab](https://colab.research.google.com/).
3. Selecciona **Archivo → Abrir notebook → GitHub**.
4. Introduce la URL del repositorio y abre `S7 Version-Estudiante-Project-ConnectaTel.ipynb`.
5. Carga los archivos CSV en el entorno de Colab.
6. Ajusta las rutas de lectura para que coincidan con la ubicación de los archivos.
7. Ejecuta las celdas en orden, desde la carga de datos hasta las conclusiones.

Si cargas los CSV dentro de una carpeta `datasets` en Colab, puedes utilizar:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

plans = pd.read_csv('/content/datasets/plans.csv')
users = pd.read_csv('/content/datasets/users_latam.csv')
usage = pd.read_csv('/content/datasets/usage.csv')
```

Estas rutas son un ejemplo y deben ajustarse a la ubicación real de los archivos.

### Opción B. Ejecución local

1. Instala Python y Jupyter Notebook.
2. Descarga el notebook desde este repositorio.
3. Obtén los tres archivos CSV originales.
4. Crea una carpeta `datasets/` en el directorio del proyecto y coloca allí los archivos.
5. Instala las dependencias necesarias:

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

6. Ajusta las rutas de carga del notebook para que correspondan a la carpeta `datasets/`.
7. Inicia Jupyter Notebook:

```bash
jupyter notebook
```

8. Abre `S7 Version-Estudiante-Project-ConnectaTel.ipynb` y ejecuta las celdas secuencialmente.

## 8. Guía de reproducción

Para reproducir el análisis correctamente:

1. Obtén los archivos originales `plans.csv`, `users_latam.csv` y `usage.csv`.
2. Verifica que los archivos tengan los nombres y las columnas esperadas.
3. Comprueba las rutas de carga antes de ejecutar el notebook.
4. Ejecuta todas las celdas en orden para que las variables y transformaciones estén disponibles.
5. Revisa los resultados de la limpieza, las estadísticas descriptivas, los outliers y la segmentación.
6. Documenta cualquier modificación de las reglas de limpieza o de las rutas.
7. Reinicia el kernel y ejecuta el notebook completo para verificar que el análisis se reproduzca sin depender de variables de sesiones anteriores.

**Nota:** los resultados pueden variar si se modifican los datasets originales o las reglas de limpieza.

## 9. Conclusiones

El proyecto permitió identificar problemas de calidad de datos, describir las distribuciones de consumo y construir segmentos de clientes por edad y nivel de uso.

La detección de valores atípicos permitió identificar usuarios con consumos extremos que requieren revisión, sin asumir que representan errores.

Los resultados proporcionan una base inicial para investigar ofertas diferenciadas y mejorar la experiencia del cliente. Como trabajo adicional, se recomienda profundizar en la relación entre consumo, plan contratado, ingresos y cancelaciones para priorizar las estrategias comerciales con mayor impacto.

10. Autoría

Proyecto desarrollado como parte del Sprint 7 de formación en análisis de datos. Estudiante Santiago Hoyos Yacup

Tecnologías utilizadas: Python, Pandas, NumPy, Matplotlib, Seaborn, Jupyter Notebook y GitHub.
