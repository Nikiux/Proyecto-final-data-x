# Patrones de uso del SITP en Bogotá

## Proyecto Final --- Data Xperience \| Universidad EAN

**Integrantes:** Nicolás Rincón, Felipe Mesa, Juan Benavides y Thomas
Serna\
**Programa:** Ingeniería de Sistemas --- Universidad EAN\
**Fecha:** septiembre de 2026

------------------------------------------------------------------------

## 1. Descripción

Este repositorio contiene el proyecto final de Ciencia de Datos sobre
los registros de validación del Sistema Integrado de Transporte Público
(SITP) de Bogotá.

El proyecto desarrolla el flujo:

**Problema → Datos → Comprensión → Limpieza → EDA → Estadística →
Visualización → Segmentación → Evaluación → Interpretación →
Conclusiones.**

La base inicial contiene **1.048.575 registros y 22 columnas**. Después
de la limpieza se obtuvieron **1.047.338 registros y 19 columnas**,
eliminando **1.237 duplicados** y las columnas `ID_Vehiculo`, `Ruta` y
`Tipo_Vehiculo`, que estaban completamente vacías.

------------------------------------------------------------------------

## 2. Problema de investigación

**¿Cómo puede la depuración y el análisis básico de los registros de uso
del SITP de Bogotá permitir la identificación de patrones de utilización
según la estación o parada, el tipo de tarjeta y el perfil del
usuario?**

Preguntas orientadoras:

1.  ¿Cuáles son las estaciones con mayor cantidad de validaciones?
2.  ¿En qué horarios se concentra la mayor cantidad de transacciones?
3.  ¿Qué tipo de tarjeta es el más utilizado?
4.  ¿Qué perfil de usuario utiliza con mayor frecuencia el sistema?
5.  ¿Existen diferencias importantes en el uso según estación, zona y
    horario?

------------------------------------------------------------------------

## 3. Fuente de los datos

La fuente institucional corresponde al conjunto de datos **Validaciones
Diarias SITP**, publicado en **Datos Abiertos Bogotá** por
**TransMilenio S.A.**

Se seleccionó por su relación directa con los registros de validación
del sistema.

------------------------------------------------------------------------

## 4. Estructura del repositorio

``` text
Proyecto-SITP-Data-Xperience/
│
├── README.md
├── informe/
│   └── Informe_Final_SITP_APA7.docx
├── presentacion/
│   └── Presentacion_Sustentacion_SITP.pptx
├── notebooks/
│   └── Codigo_Proyecto_SITP_FINAL.ipynb
├── datos/
│   └── datos_sitp.csv
├── resultados/
│   ├── resultados_hora.csv
│   ├── resultados_chi_cuadrado.csv
│   ├── resultados_clusters.csv
│   └── resultados_pca.csv
└── figuras/
    ├── estaciones_top.png
    ├── validaciones_hora.png
    ├── validaciones_franja.png
    ├── tipo_tarjeta.png
    ├── perfiles.png
    ├── distribucion_valor.png
    ├── heatmap_estaciones.png
    ├── seleccion_k.png
    └── clusters_pca.png
```

> Si el CSV es demasiado grande para GitHub, se recomienda no subirlo
> directamente. En ese caso, indicar en este README dónde obtener los
> datos y cómo configurar la ruta de carga.

------------------------------------------------------------------------

## 5. Contenido

### `informe/`

Informe académico final en formato Word. Incluye problema, objetivos,
datos, limpieza, EDA, estadística, visualizaciones, patrones, K-Means,
evaluación, PCA, conclusiones, recomendaciones y referencias.

### `presentacion/`

Diapositivas para la sustentación presencial de 10--15 minutos.

### `notebooks/`

Notebook de Google Colab/Jupyter con el código completo.

### `datos/`

Datos utilizados para ejecutar el análisis, cuando su tamaño y
condiciones de distribución permiten almacenarlos.

### `resultados/`

Tablas y archivos generados durante el análisis.

### `figuras/`

Visualizaciones utilizadas en el informe y la presentación.

------------------------------------------------------------------------

## 6. Tecnologías

-   Python
-   Google Colab / Jupyter Notebook
-   pandas
-   NumPy
-   Matplotlib
-   Seaborn
-   SciPy
-   scikit-learn

------------------------------------------------------------------------

## 7. Instalación

Para ejecución local:

``` bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn jupyter
```

También se puede ejecutar directamente en Google Colab.

------------------------------------------------------------------------

## 8. Cómo ejecutar

### Google Colab

1.  Abrir Google Colab.
2.  Subir `Codigo_Proyecto_SITP_FINAL.ipynb`.
3.  Subir o conectar el dataset.
4.  Verificar la ruta del archivo.
5.  Ejecutar las celdas en orden.
6.  Revisar las salidas, gráficas, estadísticas y resultados del modelo.

### Jupyter

``` bash
jupyter notebook
```

Después abrir `Codigo_Proyecto_SITP_FINAL.ipynb`, configurar la ruta del
dataset y ejecutar las celdas en orden.

------------------------------------------------------------------------

## 9. Flujo del análisis

### 9.1 Carga y estructura

Se carga el CSV y se verifica la dimensión inicial:

-   1.048.575 registros
-   22 columnas

También se revisan nombres, tipos de datos y valores no nulos.

### 9.2 Calidad

Se utiliza `isnull().sum()` para detectar valores faltantes.

Las columnas `ID_Vehiculo`, `Ruta` y `Tipo_Vehiculo` presentan el 100 %
de valores faltantes y se eliminan.

### 9.3 Duplicados

Se utiliza:

``` python
df.duplicated().sum()
```

Se identifican **1.237 duplicados**, que posteriormente se eliminan.

### 9.4 Limpieza

Se normalizan nombres, se limpian textos, se convierten variables cuando
corresponde, se eliminan las columnas vacías y se eliminan duplicados.

Resultado:

  Indicador          Antes     Después
  ------------ ----------- -----------
  Registros      1.048.575   1.047.338
  Columnas              22          19
  Duplicados         1.237           0

------------------------------------------------------------------------

## 10. EDA

### Estaciones

Portal Américas presenta **62.331 validaciones**, siendo la estación con
mayor cantidad dentro del conjunto depurado.

### Horarios

La hora con mayor cantidad de validaciones es **06:00**, con **201.873
registros**.

La franja **Mañana (06--11)** concentra **725.216 validaciones**.

> La franja nocturna (18--23) aparece con cero registros. Esto se
> interpreta como una característica o limitación de cobertura del
> conjunto y no como evidencia de que el SITP no opere durante la noche.

### Tipo de tarjeta

-   tullave Plus: **70,47 %**
-   tullave Básica: **29,53 %**

### Perfil

El perfil Adulto registra **524.518 validaciones**.

------------------------------------------------------------------------

## 11. Análisis estadístico

Para `Valor` se calcularon media, mediana, desviación estándar,
cuartiles, IQR, asimetría y curtosis.

Resultados principales:

-   Media: **2.946,711**
-   Mediana: **3.550**
-   Desviación estándar: **1.333,312**
-   Q1: **3.550**
-   Q3: **3.550**
-   IQR: **0**
-   Asimetría: **-1,758**
-   Curtosis: **1,089**

El IQR igual a cero requiere cautela al aplicar reglas de valores
atípicos. Los registros marcados por Tukey no se eliminan
automáticamente porque pueden representar la estructura discreta de la
tarifa y no errores.

------------------------------------------------------------------------

## 12. Chi-cuadrado

Se aplicó chi-cuadrado de independencia para estudiar:

-   Tipo de tarjeta × perfil
-   Tipo de tarjeta × franja horaria
-   Estación × franja horaria

Las pruebas presentaron **p \< .001**.

Esto indica evidencia estadística de asociación, pero **no demuestra
causalidad**.

Debido al tamaño de la muestra, los p-valores deben interpretarse junto
con el tamaño de efecto.

------------------------------------------------------------------------

## 13. K-Means

K-Means se utiliza como técnica de aprendizaje no supervisado porque el
objetivo es **agrupar estaciones** según características similares y no
predecir una etiqueta conocida.

La unidad de análisis cambia de registros individuales a estaciones.

Se utilizan características relacionadas con:

-   proporciones horarias;
-   intensidad de validaciones;
-   valor promedio.

Las variables se estandarizan con `StandardScaler`.

Se prueban valores de **K = 2 a K = 8**.

El mejor coeficiente de silueta es:

**K = 2 → Silhouette = 0,4009**

Por ello se seleccionan dos clusters.

------------------------------------------------------------------------

## 14. Resultado de la segmentación

-   Cluster 0: **75 estaciones**
-   Cluster 1: **72 estaciones**

Medianas:

  Característica                Cluster 0   Cluster 1
  --------------------------- ----------- -----------
  Validaciones por estación      5.582,00    2.718,33
  Valor promedio                 2.978,43    3.343,86

El cluster 0 presenta, descriptivamente, mayor intensidad de
validaciones.

El valor de silueta de 0,4009 representa una separación moderada, por lo
que los grupos deben interpretarse como segmentos descriptivos.

------------------------------------------------------------------------

## 15. PCA

PCA se utiliza para visualizar la segmentación en dos dimensiones.

-   Componente 1: 58,29 %
-   Componente 2: 17,95 %
-   Varianza acumulada: **76,24 %**

**K-Means genera los clusters; PCA ayuda a visualizarlos.**

------------------------------------------------------------------------

## 16. Principales hallazgos

1.  Portal Américas concentra la mayor cantidad de validaciones.
2.  Las primeras horas del día concentran gran parte de la actividad.
3.  06:00 es la hora con mayor número de validaciones.
4.  tullave Plus representa 70,47 %.
5.  Adulto es el perfil con mayor frecuencia.
6.  Existe asociación estadística entre las variables categóricas
    analizadas.
7.  K-Means identifica dos segmentos de estaciones.
8.  PCA representa 76,24 % de la varianza mediante dos componentes.

------------------------------------------------------------------------

## 17. Limitaciones

-   No existe una variable explícita de zona geográfica en las 19
    columnas finales.
-   La franja nocturna aparece con cero registros y requiere validar la
    cobertura temporal.
-   Una validación no equivale necesariamente a un usuario único.
-   K-Means produce una segmentación descriptiva y su silueta es
    moderada.
-   Las asociaciones estadísticas no permiten establecer causalidad.
-   No se debe interpretar automáticamente cada valor marcado como
    outlier como un error.

------------------------------------------------------------------------

## 18. Recomendaciones

1.  Incorporar variables geográficas o coordenadas.
2.  Validar la cobertura temporal del dataset.
3.  Investigar el significado de las diferentes tarifas.
4.  Comparar K-Means con otros métodos de clustering.
5.  Evaluar estabilidad de los clusters.
6.  Reportar tamaños de efecto junto con p-valores.
7.  Para una futura fase predictiva, definir una variable objetivo y
    utilizar modelos supervisados.

------------------------------------------------------------------------

## 19. Reproducibilidad

Para reproducir el proyecto:

1.  Obtener la misma versión del dataset.
2.  Abrir `Codigo_Proyecto_SITP_FINAL.ipynb`.
3.  Instalar las dependencias.
4.  Configurar la ruta del dataset.
5.  Ejecutar las celdas en orden.
6.  Verificar 1.047.338 registros y 19 columnas después de la limpieza.
7.  Revisar las gráficas.
8.  Revisar las pruebas estadísticas.
9.  Ejecutar K-Means.
10. Verificar K = 2 y silhouette ≈ 0,4009.
11. Ejecutar PCA.

------------------------------------------------------------------------

## 20. Entregables

De acuerdo con la rúbrica del proyecto final, este repositorio debe
contener:

-   Informe final.
-   Presentación de sustentación.
-   Notebook de Google Colab con código completo.
-   README con descripción, estructura e instrucciones de ejecución.

------------------------------------------------------------------------

## 21. Referencias

TransMilenio S.A. (2020). *Validaciones Diarias SITP* \[Conjunto de
datos\]. Datos Abiertos Bogotá.

Hunter, J. D. (2007). Matplotlib: A 2D graphics environment. *Computing
in Science & Engineering, 9*(3), 90--95.

Pedregosa, F., Varoquaux, G., Gramfort, A., et al. (2011). Scikit-learn:
Machine learning in Python. *Journal of Machine Learning Research, 12*,
2825--2830.

Rousseeuw, P. J. (1987). Silhouettes: A graphical aid to the
interpretation and validation of cluster analysis. *Journal of
Computational and Applied Mathematics, 20*, 53--65.

Waskom, M. L. (2021). seaborn: Statistical data visualization. *Journal
of Open Source Software, 6*(60), 3021.

Universidad EAN. (2026). *Estructura y calificación proyecto final*
\[Material del curso Data Xperience\].
