# Apuntes Python Machine Learning

---
## Run SQL directly in Jupyter Notebook with IPython-SQL


https://levelup.gitconnected.com/run-sql-directly-in-jupyter-notebook-with-ipython-sql-4b39c2105930



---
## Learn Jupyter Notebooks for SQL Server

https://www.sqlshack.com/learn-jupyter-notebooks-for-sql-server/


---

## Python Tutorial - For Loop with List Comprehensions

https://platzi.com/tutoriales/4227-python-fundamentos/31662-python-tutorial-for-loop-with-list-comprehensions/


~~~
# Define a list of numbers 
numbers = [1, 2, 3, 4, 5]

# Create a new list of squares using a list comprehension
squares = [number ** 2 for number in numbers]

# Print the new list
print(squares)
~~~

~~~
# Create a new list of squares for even numbers only
even_squares = [number ** 2 for number in numbers if number % 2 == 0]

# Print the new list
print(even_squares)
~~~




---

## Context Managers and Python's with Statement

https://aulas.campusmvp.com/SELF/lesson.self?LessonId=113745

~~~
file = open("hello.txt", "w")

try:
    file.write("Hello, World!")
except Exception as e:
    print(f"An error occurred while writing to the file: {e}")
finally:
    # Make sure to close the file after using it
    file.close()
~~~


~~~
with expression as target_var:
    do_something(target_var)

~~~





---
## leer datos desde el portapapeles


~~~



~~~


~~~
import pandas as pd
calidad_aire = pd.read_clipboard()
calidad_aire.describe()
~~~





---

## Missing Values With Pandas

https://medium.com/swlh/data-science-for-beginners-how-to-handle-missing-values-with-pandas-73db5fcd46ec


~~~
import pandas as pd
pd.read_excel('Students_Scores.xlsx')

missing_value_forms=['?','Nil']
df= pd.read_excel('Students_Scores.xlsx',na_values= missing_value_forms, index_col= 'Student ID')
df

df.isnull()

~~~


---
### 3│Filtrar dataframe en pandas Python, selección de filas y columnas python - método .loc y .iloc.

https://www.youtube.com/watch?v=0MEoGE1Cd04


~~~



~~~


---
## Automatizar Excel con Python | Leer y procesar archivos con Pandas

https://www.youtube.com/watch?v=JL9RMCS4Sho



---
## 7. Cómo Agrupar Datos en Python con GroupBy: Tutorial Completo con Pandas

https://www.youtube.com/watch?v=aUv2UygYKmI




---
## OPENPYXL | Cómo trabajar en EXCEL desde PYTHON (muy FÁCIL)

https://www.youtube.com/watch?v=WMPZMeAQX3Q





---
## CURSO de PYTHON con PANDAS Para Ciencia de Datos - ESTRUCTURA DE DATOS

https://www.youtube.com/watch?v=loqDUi749j0&list=PLg9145ptuAig5cwvUCn9FNSUJyXBiFcVg&index=4




---

## Tips, ideas, notas para graficas sacadas de los apuntes del cursos machine learing

los conteos de un conjunto de datos en phyton con value_counts()


---

## Tutorial: ANÁLISIS EXPLORATORIO DE DATOS con Python


https://www.youtube.com/watch?v=wBu0hQQVdcE



---
## Tutorial: MANEJO DE DATOS CATEGÓRICOS FALTANTES con Python, Pandas y Scikit-Learn

https://www.youtube.com/watch?v=G3tNCSQUoXw




---
## Tutorial: ¡PANDAS DESDE CERO!

https://www.youtube.com/watch?v=qaetvFaYOWM

Codificando Bits



---

## Tutorial: LIMPIEZA DE DATOS con Python y Pandas

https://www.youtube.com/watch?v=bGnD1Ki7j-g


Codificando Bits

---
## Máquinas de Soporte Vectorial | Cómo funcionan las SVM | Código en python

https://www.youtube.com/watch?v=XyH8bdv_DSw




---


## ¿Cómo funciona SVM?

https://www.youtube.com/watch?v=kl6tyEi5eso


---
## MÁQUINAS DE SOPORTE VECTORIAL: ¡explicación COMPLETA!

https://www.youtube.com/watch?v=Xbd8T-JoGPQ


---
## 5. Dominando el Arte de la Limpieza de Datos en Big Data

https://www.youtube.com/watch?v=fpF-GJn4kXk

---

## Curso COMPLETO de IA desde Cero (con PYTHON)!! : Limpieza de datos - Modulo 1


https://www.youtube.com/watch?v=QLKPEOl5oLA



~~~



~~~




---
## Curso COMPLETO de IA desde Cero (con PYTHON)!! : Limpieza de datos (PARTE 2) - Modulo 1

https://www.youtube.com/watch?v=QTn-H3b9lg0


---
## Tutorial: ¡SCIKIT-LEARN DESDE CERO!

https://www.youtube.com/watch?v=qUjIybMkXBs

Codificando Bits


~~~





~~~






---
## Tutorial: ¿cómo ALMACENAR Y LEER un modelo en Scikit-Learn?

https://www.youtube.com/watch?v=jrECkCRpU4s

Codificando Bits

---
## Tutorial: AFINACIÓN DE HIPER-PARÁMETROS en Scikit-Learn

https://www.youtube.com/watch?v=hcbVLNZ2gAQ

Codificando Bits

---
## ¿Cómo manejar un dataset DESBALANCEADO en Machine Learning?

https://www.youtube.com/watch?v=8CE4I8o4ZM0

Codificando Bits
---

## ¿Cómo manejar los VALORES EXTREMOS en nuestros datos?

https://www.youtube.com/watch?v=GiX51cG-tO4

Codificando Bits

---
## ¿Cómo manejar los DATOS FALTANTES?: guía completa


https://www.youtube.com/watch?v=ARwHkq4t2q0

Codificando Bits

---

## Tutorial: MANEJO DE DATOS CATEGÓRICOS FALTANTES con Python, Pandas y Scikit-Learn

https://www.youtube.com/watch?v=G3tNCSQUoXw

Codificando Bits

---

## Los sets de entrenamiento, validación y prueba

https://www.youtube.com/watch?v=79K93XBOsIg

Codificando Bits

---
## Clasificación con Árboles de Decisión ¡EN 15 MINUTOS!

https://www.youtube.com/watch?v=kqaLlte6P6o


Codificando Bits

---
## Regresión con Árboles de Decisión: el algoritmo CART

https://www.youtube.com/watch?v=2Miw4bjzSF0


Codificando Bits

---

## La Matriz de Confusión

https://www.youtube.com/watch?v=haEWWO0b42Y


datos balanceados y desbalanceados



Codificando Bits


Matriz de confusion para clasificacion binaria

positivo    ---   negativo

Categoria real | Categoria Predicha |      esto es un...        |
 positivo      |   positivo         |     Verdadero Positivo VP |
 positivo      |   negativo         |     Falso Negativo     FN |  DESACIERTO
 negativo      |   negativo         |     Verdadero Negativo VN |
 negativo      |   positivo         |        Falso Positivo  FP |  DESACIERTO


c p                 Categorias reales
a r          |  normal    |  anormal   | 
t e   Normal |            |            |    
e d   Anormal|            |            |
g i
o c
r h
i a
a s
s


Matriz de confusion para clasificacion multiples clases






Limitaciones de la matriz de confusion



Habria que ir a las metricas Precision, Recall y F-Score


~~~


~~~



---

## PRECISION, RECALL Y F-SCORE: ¿qué son y cuándo usarlos?

https://www.youtube.com/watch?v=H8FSfqxRWmA

relacionado con la exactitud de un modelos y la matriz de Confusion, mas metricas porque la matriz de confusion no es suficiente para medir la precision(accuracy) o exactitud de los modelos

tambien relacionado con set de datos desbalanceados

Codificando Bits
















~~~


~~~



---

## 5 pasos para APRENDER MACHINE LEARNING desde cero

https://www.youtube.com/watch?v=wYyAgqx2eSQ&list=PL9E7H1rzXKFKiOmHB9rLrOoHDQaSMlzKI


Codificando Bits

---



---



---

## Los diferentes ALGORITMOS DEL MACHINE LEARNING

https://www.youtube.com/watch?v=XNWKJsDNScw

Codificando Bits

---
### Tutorial: ¿Por qué y cuándo ESCALAR los datos?

https://www.youtube.com/watch?v=pyurbDGzDic


Codificando Bits


---

## Curva ROC y AUC

https://www.youtube.com/watch?v=_-THb5I9QGg


Codificando Bits




---

## Validación cruzada y k-fold cross-validation

https://www.youtube.com/watch?v=bpZa2mAiXS8


Codificando Bits



---

## Cross-validation (o Validación Cruzada) para Evaluar Modelos de Machine Learning con Python

https://www.youtube.com/watch?v=Qnth2VXopLg&t=5s


Codigo Maquina

Conjunto de datos para entrenamiento, validacion y prueba o test
~~~



~~~

Evaluacion con validacion cruzada

~~~
import pandas as pd

from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import cross_val_score

personas = pd.read_csv("salario.csv")

bosque = RandomForestClassifier()

bosque.fit(personas[["edad","estudio"]].values,personas[['ingreso'].values)

# evaluacion de todos los datos, y el score vamos a tener, todos los datos se cogen , no se separan en datos para estudio, y datos para test, si no que todo los datos se utilizan para crear el modelo, cosaa que no es correcta, hay que dividirlo en dos grupos, datos para estudio y datos para test

print (bosque.score(personas[['edad','estudio']].values,personas['ingreso'].values))

# da un valor muy alto de accuracy

# ahora vamos a ver otra forma con la cross validacion

print(cross_val_score(bosque,personas[['edad','estudio']].values,personas["ingreso"].values,cv=5))


print(cross_val_score(bosque,personas[['edad','estudio']].values,personas["ingreso"].values,cv=5).mean())



~~~





---

## Las Mejores Métricas para Evaluar Modelos de Regresión con Scikit-Learn: R2, MSE, RMSE, MAE y otras

https://www.youtube.com/watch?v=9IZ6OPQWtpw

Codigo Maquina


### Metricas

### Error Absoluto maximo (M)

~~~

from sklearn.metrics import max_error

y_verdadero = [1,2,3,4,5]

y_predicho = [1,2,3,4,-5]

max_error(y_verdadero,y_predicho)


~~~

### Error absoluto medio (mean absolute error - MAE)

~~~
from sklearn.metrics import mean_absolute_error

y_verdadero = [1,2,3,4,5]
y_predicho = [1,2,3,4,-5]

mean_absolute_error(y_verdadero,y_predicho)

~~~

### Error cuadratico medio (mean squared error - MSE)  la mas utilizada

~~~

from sklearn.metrics import mean_squared_error

y_verdadero = [1,2,3,4,5]
y_predicho = [1,2,3,4,-5]

mean_squared_error(y_verdadero,y_predicho)

~~~

### Suma de los cuadrados de los residuos (RSS) 

~~~

from sklearn.metrics import mean_squared_error

y_verdadero = [1,2,3,4,5]
y_predicho = [1,2,3,4,-5]

mean_squared_error(y_verdadero,y_predicho)


~~~

### Raiz cuadrada del error cuadratico medio (RMSE) es muy utilizada

~~~

from sklearn.metrics import mean_squared_error

y_verdadero = [1,2,3,4,5]
y_predicho = [1,2,3,4,-5]

mean_squared_error(y_verdadero,y_predicho,squared=False)

~~~

### R^2 (Coeficiente de determinacion) es parecido al coeficiente relacion solo aplique para modelos de regresion lineal
### no la podemos utilizar para modelos de regresion no lineal

~~~


from sklearn.metrics import r2_score

y_verdadero = [1,2,3,4,5]
y_predicho = [1,2,3,4,-5]

r2_score (y_verdadero,y_predicho)



~~~


---

## Regresión Logística con Python

https://www.youtube.com/watch?v=Z-bFsyiQxb0


Codigo Maquina



### Funcion Logistica Estandar

~~~

import numpy as np
import matplotlib.pyplot as plt
import math

# creamos una funcion logisticas vectorial

logistica = np.frompyfunc(lambda b0,b1,x:
     1/(1+math.exp(-(b0+b1*x))),3,1)



# graficamos la funcion logistica con diferentes pendientes

plt.figure(figsize=(8,4))

# grafica de dispersion

plt.scatter(np.arange(-5,5,0.1),logistica(0,1,np.arange(-5,5,0.1)),color="green")

plt.scatter(np.arange(-5,5,0.2),logistica(0,1,np.arange(-5,5,0.1)),color="gold")

plt.scatter(np.arange(-5,5,0.3),logistica(0,1,np.arange(-5,5,0.1)),color="red")




plt.title("Funcion logistica estandar - diferentes pendientes",fontsize=14.0)
plt.ylabel("Probabilidad",fontsize=13.0)
plt.xlabel("Valores",fontsize=13.0)

plt.show()


~~~

vamos a verlo con unos datos aplicar a este modelo de regresion logistica


### Taquicardia: Probabilidad y Clase


~~~

# Persona Normal con 60 a 100 latidos por minuto
# Person con Taquicardia de hasta 220 latidos por minuto

personas_normal = [65,70,80,80,80,90,95,100,105,110]

personas_taquicardia = [105,110,110,120,120,130,140,180,185,190]

# Graficamos una funcion Logistica

plt.figure(figsize=(6,4))

# y = b0 + b1 * x
#
# y = -46.68057196 + 0.42460226 * x

plt.scatter(np.arange(60,200,0.1),logistica(-46.68057196,0.42460226,np.arange(60,200,0.1)))

# Graficamos la frecuencia cardiaca de las personas

plt.scatter(presonas_normal,[0]*10,marker="o",c="green",s=250,label="Normal")

plt.scatter(personas_taquicardia,[1]*10,marker="o",c="red",s=250,label="Taquicardia")

individuos=[80,110,180]

probabilidades = logistica(-46.6805716,0.42460226,individuos)

plt.scatter(individuos,probabilidades,marker="*",c="darkorange",s=500)

plt.text(individuos[0]+7,0.05,"%0.2f" % probabilidades[0],size=12,color="black")

plt.text(individuos[1]+7,0.48,"%0.2f" % probabilidades[1],size=12,="black")

plt.text(individuos[2]+7,0.90,"%02.f" % probabilidades[2],size=12,color="black")

plt.text(0,1,"TAQUICARDIA",size=12,color="red")

plt.ylabel("Probabilidad de Taquicardia",fontsize=13.0)
plt.xlabel("Frecuencia cardiaca (Latidos por minuto)",fontsize=13.0)
plt.legend(bbox_to_anchor=(1,0.2))
plt.show()





~~~

### Maxima verosimilitud



~~~
plt.figure(figsize(6,4))

for b1 in np.arange(0.35,0.49,0.025):
    plt.scatter(np.arange(60,200,0.1),logistica(-46.6805719,b1,np.arange(60,200,0.1)),label="b_1=%0.2f" % b1)

# Graficamos la frecuencia cardiaca de las personas

plt.scatter(personas_normal,[0]*10,marker="o",c="green",s=250,label="Normal")

plt.scatter(personas_taquicardia,[1]*10,marker="o",c="red",s=250,label="Taquicardia")

plt.title("Maxima verosimilitud", fontsize=18.0)
plt.text(0,1,"TAQUICARDIA",size=12, color="red")
plt.text(0,0,"NORMAL",size=12,color="red")
plt.ylabel("Probabilidad de Taquicardia",fontsize=13.0)
plt.xlabel("Frecuencia cardiaca (latidos por minuto)",fontsize=13.0)
plt.legend(bbox_to_anchor=(1,1))
plt.show()

~~~

### Modelo de Regresion Logistica


~~~
from sklearn.linear_model import LogisticRegression

from sklearn.model_selection import train_test_split

frecuencias_cardiacas = [[65],[70],[80],[80],[80],[90],[95],[100],[105],[110],[105],[110],[110],[120],[120],[130],[140],[180],[185],[190]]

clase = [0,0,0,0,0,0,0,0,0,0,
         1,1,1,1,1,1,1,1,1,1]

# Creamos conjuntos de entrenamiento y de prueba del modelo

datos_entrena,datos_prueba,clase_entrena,clase_prueba = train_test_split(frecuencias_cardiacas,clase,test_size=0.30)

# Creamos el modelo de regresion logistica

modelo = LogisticRegression().fit(datos_entrena,clase_entrena)

np.set_printoptions(suppress=True)

print(modelo.predict(datos_prueba))

print(modelo.predict_proba(datos_prueba))
print(modelo.score(datos_prueba,clase_prueba))

print(modelo.intercept_,modelo.coef_)



~~~


---

## Escalamiento, Normalización y Estandarización de Datos con Python para Ciencia de Datos

https://www.youtube.com/watch?v=-VuR14Qyl7E


Codigo Maquina



~~~

import pandas as pd
import matplotlib.pyplot as plt

frin sklearn import preprocessing

datos = pd.read_csv("datos_personas.csv")

datos





~~~






---

## Visualización de Datos usando Matplotlib de Python - Curso introductorio a la creación de gráficas

https://www.youtube.com/watch?v=foLHkB6W_Ww


Codigo Maquina

CodigoMaquina_plt_pruebas_01.ipynb


~~~
import matplotlib.pyplot as plt

eje_x = ["a","b","c","d","e"]

datos = [10,20,30,40,50]

plt.plot(eje_x,datos)
plt.show()




~~~



~~~
import matplotlib.pyplot as plt

eje_x = ["a","b","c","d","e"]

datos1 = [10,20,30,40,50]
adtos2 = [20,30,40,50,60]


plt.plot(eje_x,datos1)
plt.plot(eje_x,datos2)
plt.show()




~~~




~~~

import numpy as np

años = ["2011","2012","2013","2014","2015","2016","2017","2018","2019","2020"]

nivel1 = np.random.rand(10)*100
nivel2 = np.random.rand(10)*200 + 100
nivel3 = np.random.rand(10)*300 + 200
nivel4 = np.random.rand(10)*400 + 300
nivel5 = np.random.rand(10)*500 + 400





~~~



~~~









~~~

---

## Descubre cómo Visualizar Datos Categóricos con Seaborn y Python: gráficas de violín, enjambre y ➕

https://www.youtube.com/watch?v=ncfPK06nKA8

Codigo Maquina

CodigoMaquina_Visualizar_Seaborn.ipynb

caplot (categoricas) (*)
displot (distribuciones)
relplot (relacional)

catplot(Categorias)
  - dispersion  
  - distribuciones
  - Estimacion
  


---

## Explora y Visualiza Relaciones Estadísticas con Seaborn de Python: Gráficas de Línea y Dispersión

https://www.youtube.com/watch?v=Mq4lF0eEw8s


Codigo Maquina

CodigoMaquina_Visualizar_Relaciones_estadisticas.ipynb


caplot (categoricas) 
displot (distribuciones)
relplot (relacional) (*)


---

## Imputación (o Manejo de Datos Faltantes) con Python

https://www.youtube.com/watch?v=XiKYdHUsgyM

Codigo Maquina

CodigoMaquina_Manejo_Datos_Faltantes.ipynb




---
## Maneja y Analiza Datos con DataFrames de Pandas y Python

https://www.youtube.com/watch?v=DjQyHmy9AqQ&t=312s

Codigo Maquina

---
## Series de Pandas: El Componente Principal de los DataFrames para Analizar Datos con Python
https://www.youtube.com/watch?v=E7Tt458sTUE&t=912s

Codigo Maquina

CodigoMaquina_SeriesPandas.ipynb

---
## Análisis de Componentes Principales (PCA) para Reducir la Dimensionalidad de Datos usando Python

https://www.youtube.com/watch?v=x-7BHjMA15M

Codigo Maquina


CodigoMaquina_Analisis_Componentes_Principales_PCA.ipynb

---

## Reshape -1, 1 and Reshape 1, -1 in Python NumPy | Module NumPy Tutorial - Part 07

https://www.youtube.com/watch?v=yDXNPyxDb0M



---

## reconocimiento de imágenes con IA - 01 - Convoluciones y filtros

https://www.youtube.com/watch?v=AwTH_0yW9_I



---
## Descifrando el Misterio: Redes Neuronales Convolucionales (CNNs) con Python y Tensorflow

https://www.youtube.com/watch?v=zBqnWfTwCgc

Codigo Maquina



---


## ¿Cómo visualizar imágenes con matplotlib?

https://www.youtube.com/watch?v=VGpRB3juwsQ&list=PLbk60veMSVKtrFAhp-R_uMH4wlFp5RW6E


DiMathData

habla sobre el dataset nmist

---

## ¿Cómo hacer una matriz de imagenes tomadas de un dataset?

https://www.youtube.com/watch?v=RRPDcysd5mQ


DiMathData

habla sobre el dataset nmist y como graficar las imagenes con mas detalle que el video anterior


---


¿Cómo entrenar un clasificador multiclase con SGDClassifier de Sklearn?

https://www.youtube.com/watch?v=__0tQhvRR20


DiMathData

aplica este modelo SGDClassifier  al conjunto de datos mnist


~~~
fig,ax = plt.subplots(1,5)
for indice,instancia in enumerate(X_test[:5]):
    ax[indice].imshow(instancia.reshape([28,28],cmap='binary'))


~~~



---




---