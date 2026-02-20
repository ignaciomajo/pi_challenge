# **BigMart Sales - Pi Challenge**

<img width="1024" height="695" alt="Gemini_Generated_Image_y3ya0qy3ya0qy3ya" src="https://github.com/user-attachments/assets/4dcc8ba3-8e2e-4b8a-a9d7-bc5bdbfe45aa" />

---

## Índice 📋

1. Descripción del proyecto
2. Acceso al proyecto
3. Etapas del proyecto
4. Catálogo de datos
5. Resultados y conclusiones
6. Implementación y Uso de Predicciones
7. Tecnologías utilizadas
8. Agradecimientos
9. Desarrolladores del proyecto

---


## 1. Descripción del Proyecto 📚

### **Contexto del Negocio** 

Big Mart es una cadena minorista que busca optimizar su cadena de suministro y estrategias de inventario. El desafío consiste en comprender las propiedades de los productos y los establecimientos que desempeñan un papel crucial en el aumento de las ventas.

### **Objetivo** 

Construir un modelo predictivo de regresión para estimar las ventas de los productos en las distintas tiendas de la cadena, permitiendo identificar los factores clave que impulsan el rendimiento comercial.

### **La Solución** 

Se desarrolló un modelo basado en Random Forest Regressor, optimizado mediante técnicas de selección de características (Feature Selection) y ajuste de hiperparámetros (Randomized Search). La solución final destaca por su parsimonia, utilizando solo las variables de mayor impacto para garantizar rapidez y eficiencia en entornos productivos.

---

## 2. Acceso al Proyecto 📂

Para obtener el proyecto tienes dos opciones:

1. Clonar el repositorio utilizando la línea de comandos. Solo debes dirigirte al directorio donde deseas clonar el mismo e ingresar el comando:<br><br>
   `git clone https://github.com/ignaciomajo/pi_challenge`

2. O puedes descargarlo directamente desde el repositorio en GitHub en el siguiente enlace:<br>

   [https://github.com/ignaciomajo/pi_challenge](https://github.com/ignaciomajo/pi_challenge)

   Esto te llevará a la siguiente pantalla, donde deberás seguir los siguientes pasos:

<img width="1786" height="677" alt="image" src="https://github.com/user-attachments/assets/eb801d36-7237-48bd-b21b-2acb84074a96" />

   
Esto descargará un archivo comprimido `.zip`, que podrás alojar en el directorio que desees.


### **NOTA**:

El proyecto incluye una carpeta /modelos con los artefactos necesarios (.pkl) y una función apply_model diseñada para procesar nuevos datos de forma automatizada.

---
## 3. Etapas del Proyecto 📝

1. **Descripción del Notebook**
2. **Configuraciones**
   - Importación de Librerías
   - Paths
   - Paleta de Colores del Proyecto
3. **Extracción de Datos**
   - Extracción de Datos
   - Exploración Inicial
   - Tratamiento de Valores Faltantes
   - Normalización de Datos
4. **Análisis Exploratorio de Datos (EDA)**
   - Productos
   - Tiendas
5. **Modelado**
   - Baseline Model - OLS
   - Random Forest Regressor
6. **Conclusiones**
   - Conclusiones de Negocio
   - Amplificación del Análisis
   - Estrategias de Negocio
7. **Artefactos**
8. **Procesamiento conjunto de prueba**


---
## 4. Catálogo de Datos


| Variable	                | Tipo de dato        | Definición Funcional	                                      |
|---------------------------|---------------------|--------------------------------------------------------------|
| Item_Identifier           | Categórico Nominal  | ID único del producto                                        |
| Item_Weight               | Numérico Continuo   | Peso del producto                                            |
| Item_Fat_Content          | Categórico Nominal  | Contenido de grasa (Low Fat / Regular)                       |
| Item_Visibility           | Numérico Continuo   | % del área de exhibición total en la tienda                  |
| Item_Type                 | Categórico Nominal  | Categoría del producto                                       |
| Item_MRP                  | Numérico Continuo   | Precio máximo de venta al público (List Price)               |
| Outlet_Identifier         | Categórico Nominal  | ID único de la tienda                                        |
| Outlet_Establishment_Year | Numérico Discreto   | Año de apertura de la tienda                                 |
| Outlet_Size               | Categórico Ordinal  | Tamaño de la tienda (High, Medium, Small)                    |
| Outlet_Location_Type      | Categórico Ordinal  | Tipo de ciudad/región                                        |
| Outlet_Type               | Categórico Nominal  | Tipo de establecimiento                                      |


#### **Target**

| Variable          | Tipo de dato      | Descripción Funcional                                  | 
|-------------------|-------------------|--------------------------------------------------------| 
| Item_Outlet_Sales | Numérico Continuo | Ventas del producto en la tienda (Variable objetivo)   |


---
## 5. Resultados y Conclusiones


A través de un proceso de optimización iterativa, se seleccionó el modelo RandomForest 6 como la solución definitiva. Este modelo logra un equilibrio óptimo entre precisión estadística y eficiencia computacional.

| Model	        | Train R-Squared	    | Test R-Squared   | R-Squared Variability	  | RMSE Test   | 	MAE    |
|---------------|---------------------|------------------|--------------------------|-------------|----------|
| RandomForest  | 0.7434	            | 0.7445	         | 0.0011	                  | 0.5183	    | 720.81   |

#### **Nota:**

El MAE (Error Medio Absoluto) de 720.81 representa el error promedio en la moneda original, permitiendo una interpretación clara del impacto financiero de las predicciones.

### Variables con mayor influencia

Se determinó que el 98.91% de la predicción está impulsada por:

* Item_MRP (Precio)
* Outlet_Type (Tipo de Tienda)
* Outlet_Size (Tamaño de la tienda)

### Insights de Negocio

* **El Precio como Driver:** El Item_MRP es el principal determinante de ventas, pero su efectividad depende del formato de la tienda.
* **Dualidad de Negocio:** Se identifican dos comportamientos claramente diferenciados entre Grocery Stores y Supermarkets, variando significativamente en diversidad de inventario y volumen de facturación.
* **Eficiencia en Datos:** Se comprobó que variables como el tipo de producto, peso o contenido graso no aportan valor predictivo significativo, permitiendo simplificar los procesos de recolección de datos y reducir el ruido en el modelo.


---
## 6. Implementación y Uso de Predicciones 🚀

Para facilitar la adopción del modelo por parte de los equipos de Big Mart, se desarrolló una solución modular que permite procesar nuevos datos de forma masiva.

### Uso de la función apply_model

El proyecto incluye la función apply_model(df, ruta_objetos, ruta_guardado), la cual automatiza el flujo completo de:

1. Carga de artefactos (Modelo, Preprocesador y Metadatos).
2. Selección y limpieza de variables críticas.
3. Transformación de datos y predicción en escala logarítmica.
4. Reversión de la transformación para entrega de valores en unidades monetarias reales.

### Localización de Resultados

Cada ejecución de la función genera un archivo de salida en la carpeta /results (o la ruta especificada).

* **Formato de archivo:** sales_projection_YYYYMMDD.csv
* **Contenido:** El archivo original de entrada enriquecido con la columna Sales_Projection, que contiene la estimación de ventas para cada registro.

El uso del timestamp en el nombre del archivo garantiza un historial organizado de las proyecciones realizadas, facilitando auditorías y comparativas temporales de rendimiento.

### Presentación de negocios

En adición, el proyecto cuenta con una presentación de negocios donde se explica el proceso de investigación desarrollado y los hallazgos y conclusiones obtenidas.
El mismo se encuentra en el directorio 📂 **/reports** del presente repositorio.

---
## 7. Tecnologías Utilizadas 🛠️

* `Python`
* `Jupyter`
* `Git and GitHub`

---
## 8. Agradecimientos 🤝

Quiero agradecer a Pi Consulting por proporcionar el entorno para el desarrollo del presente proyecto.

<img width="394" height="128" alt="imagen_pi" src="https://github.com/user-attachments/assets/4030602c-c092-4172-93cd-ae40349d2b46" />


---
## 9. Desarrollador del Proyecto 👷

![imagen-readme](https://github.com/user-attachments/assets/f3fe7864-f839-4d6f-8a05-4bc2ec5ca7c8)


* **| Ignacio Majo | Data Scientist |**
 

📫 Contacto: ignacio.majoo@gmail.com | 💻[LinkedIn](https://www.linkedin.com/in/ignacio-majo/)
