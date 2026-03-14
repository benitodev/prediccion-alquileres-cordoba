# Córdoba Rent Price Prediction

Proyecto de ciencia de datos orientado a la **predicción de precios de alquiler de departamentos en Córdoba Capital (Argentina)** a partir de un dataset propio construido mediante **web scraping** y enriquecido con **geocodificación**.

El notebook desarrolla un flujo completo de trabajo:
- carga del dataset desde Google Sheets,
- análisis exploratorio de datos (EDA),
- limpieza y preprocesamiento,
- feature engineering con variables geoespaciales,
- clustering geográfico con K-Means,
- entrenamiento de un modelo de regresión,
- evaluación e interpretación de resultados.

## Objetivo

Estimar el precio de alquiler de una propiedad utilizando variables físicas y de ubicación, incorporando además señales espaciales derivadas de coordenadas y distancias a puntos de interés de la ciudad.

## Dataset

El dataset fue elaborado a partir de publicaciones reales de alquiler en Córdoba Capital.

Variables principales utilizadas:
- `price`
- `room`
- `bathroom`
- `square_meter`
- `neighborhood`
- `neighborhood_latitude`
- `neighborhood_longitude`

Según las salidas guardadas en el notebook:
- **1044** registros originales
- **896** registros finales luego de eliminar filas sin geolocalización útil

## Metodología

### 1. Carga y exploración
El notebook carga el dataset desde una hoja pública de Google Sheets y realiza una inspección inicial de tipos, valores faltantes y distribuciones.

### 2. Análisis exploratorio
Se analizan:
- distribución de precios,
- metros cuadrados,
- cantidad de ambientes y baños,
- relación entre precio y coordenadas,
- correlaciones numéricas.

### 3. Limpieza de datos
Se eliminan registros sin latitud/longitud válidas, ya que la ubicación es una parte central del problema.  
También se verifica la presencia de duplicados.

### 4. Feature engineering
Se construyen variables que agregan valor predictivo:
- **clusters geográficos** con K-Means (`cluster_zone`),
- distancia al **Centro**,
- distancia a **Ciudad Universitaria (UNC)**,
- distancia a **Nuevocentro Shopping**.

### 5. Modelado
Se entrena un modelo **Gradient Boosting Regressor** sobre una transformación logarítmica del precio.

### 6. Evaluación
Métricas obtenidas en el notebook:
- **MAE:** 115744.55 ARS
- **R²:** 0.6149

Estos resultados muestran un desempeño razonable para una primera versión del modelo, especialmente considerando la ausencia de variables de calidad intrínseca del inmueble (amenities, estado, antigüedad, etc.).

## Principales hallazgos

- La **ubicación** tiene un peso determinante en el precio.
- Los **clusters geográficos** ayudan a capturar zonas de distinto valor inmobiliario.
- El modelo funciona mejor en el segmento general del mercado que en propiedades premium o de ultra-lujo.
- El análisis de residuos sugiere que mejorar la calidad del dataset puede aportar más valor que cambiar de algoritmo.


## Cómo ejecutar

1. Abrir el notebook en Google Colab o Jupyter.
2. Verificar que el enlace al dataset publicado en Google Sheets siga disponible.
3. Ejecutar las celdas en orden.

## Posibles mejoras

- Incorporar texto de descripción de las publicaciones para extraer amenities y señales de calidad.
- Agregar variables como antigüedad, disposición y servicios del edificio.
- Comparar contra modelos adicionales y validar con cross-validation.
- Exportar el pipeline para inferencia sobre nuevas propiedades.

## Autor

Proyecto personal orientado a portfolio y práctica de machine learning aplicado al mercado inmobiliario.
