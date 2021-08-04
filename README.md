# Nutrition-Health-Analysis


Objetivo del proyecto:

Identificación de potenciales pacientes (de edad adulta) para una consulta de nutrición, mediante el análisis de un gran listado de características físicas, mentales y hábitos de consumo.
Realizar segmentación de estos mediante la realización de un score que nos permita catalogar pacientes de tipo A,B,C y D.


Dataset:
Extraido de Kaggle:https://www.kaggle.com/cdc/national-health-and-nutrition-examination-survey?select=medications.csv
Base de datos de NHANES (National Health and Nutrition Examination Survey)


Workflow:


1. Creación del dataset:
- Unión de las tablas:
      Demográfico
      Laboratorio
      Cuestionario
      Información Nutricional

-Descodificación de las variables: Las variables categóricas estaban codificadas, se les da un nombre apropiado y entendible.
- Filtración de datos seleccionando todos los encuestados mayores a 16 años,tras la eliminación de todos los pacientes menores de 16 años el data set queda con alrededor de 6.066 observaciones.


2.EDA:

- Representación gráfica de la distribución de los datos de las diferentes variables.
- Análisis de Correlaciones sobre variables clave como el ‘IMC’ (Indice de Masa Corporal) e identificación de Colinealidad.
- Identificación de los dtypes.
- Reconocimiento de % de NaN del dataset.


3. Data Wrangling:

- Eliminación de outliers: Las variables categóricas tenían asignados valores elevados para aquellos casos en los que se rechazara la pregunta

- Data cleaning:
      Fillna con 0 para aquellas variables con valores binarios (corresponde a los hábitos de las personas se entiende que si el valor es nulo la persona no lo realiza)
      Eliminación de aquellas variables innecesarias (colinealidad, baja correlación, datos no representativos de la realidad)

5. Data Preprocessing:

- Data Scaling: Transformación de variables con falsos datos numéricos a categóricos

- Feature Engineering:
    Creación de nuevas variables, conversión de unidades de medida, etc.
    Creación Score de paciente y segmentación de los datos:
    
Selección de los candidatos:

  - Realización de análisis médico, para todas aquellas personas que no tengan un IMC dentro de los parámetros saludables (18-25) se preseleccionaran como potenciales 
  pacientes de consulta.
  - Todas aquellas personas que se establecieron como objetivo cambiar su peso para el próximo año y no lo consiguieron
  - Todas aquellas personas que actualmente hayan declarado la voluntad para cambiar su peso actual
  
Cálculo del Score:

  - Estandarización de todas las variables numéricas.
  - Análisis de las correlaciones de las variables independientes con la variable objetivo(‘POTENCIAL PACIENTE’), en este caso, el numero de personas que tienen la voluntad 
  de cambiar su peso actual. Utilización del R2 para utilizarlo como ponderación del score total
  - Preselección de aquellas variables a tener en consideración para calcular el Score.
  - Multiplicar los valores estandarizados por la ponderación de los valores (R2 sobre variable objetivo) y realizar sumatorio de estas

- Data Encoding: Transformación de variables categóricas a numéricas binarias (0,1)


6. Model Training and score:

- PCA: Análisis de la separabilidad de los datos según los segmentos de potencial paciente (A,B,C,D)

- Creación de Pipeline: Evaluando diferentes modelos y seleccionando Logistic Regression como el modelo más preciso en sus predicciones.

- Fine Tunning: Se han optimizado los parámetros, mejorando así la precisión de los resultados finales del modelo.


Insights:

Perfil Segmento A
Genero: Hombre   Estado Civil: Soltero   Ingresos Fam.: 45.000 -54.999 $   Activ. Fisica/dia (min): 24   Estado Peso: Obeso  Fast food/7dias: 2,7  Diabetes_2=1 

Perfil Segmento B
Genero: Hombre   Estado Civil: Casado   Ingresos Fam.: 55.000 -64.999 $   Activ. Fisica/dia (min): 26   Estado Peso: Sobrepeso  Fast food/7dias: 2,3  Diabetes_2=0,4

Perfil Segmento C
Genero: Mujer   Estado Civil: Casado   Ingresos Fam.: 55.000 -64.999 $   Activ. Fisica/dia (min): 27   Estado Peso: Sobrepeso  Fast food/7dias: 2  Diabetes_2=0,2

Perfil Segmento D
Genero: Mujer   Estado Civil: Casado   Ingresos Fam.: 65.000 -74.999 $   Activ. Fisica/dia (min): 30   Estado Peso: Saludable  Fast food/7dias: 1,5  Diabetes_2=0






