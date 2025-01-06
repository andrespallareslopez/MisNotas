# Apuntes Python Machine Learning

---
## Run SQL directly in Jupyter Notebook with IPython-SQL


https://levelup.gitconnected.com/run-sql-directly-in-jupyter-notebook-with-ipython-sql-4b39c2105930



---
## Learn Jupyter Notebooks for SQL Server

https://www.sqlshack.com/learn-jupyter-notebooks-for-sql-server/


---

Python Tutorial - For Loop with List Comprehensions

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

Tutorial: ANÁLISIS EXPLORATORIO DE DATOS con Python


https://www.youtube.com/watch?v=wBu0hQQVdcE



---
Tutorial: MANEJO DE DATOS CATEGÓRICOS FALTANTES con Python, Pandas y Scikit-Learn

https://www.youtube.com/watch?v=G3tNCSQUoXw




---
Tutorial: ¡PANDAS DESDE CERO!

https://www.youtube.com/watch?v=qaetvFaYOWM

Codificando Bits



---

Tutorial: LIMPIEZA DE DATOS con Python y Pandas

https://www.youtube.com/watch?v=bGnD1Ki7j-g


Codificando Bits

---
Máquinas de Soporte Vectorial | Cómo funcionan las SVM | Código en python

https://www.youtube.com/watch?v=XyH8bdv_DSw




---


¿Cómo funciona SVM?

https://www.youtube.com/watch?v=kl6tyEi5eso


---
MÁQUINAS DE SOPORTE VECTORIAL: ¡explicación COMPLETA!

https://www.youtube.com/watch?v=Xbd8T-JoGPQ


---
5. Dominando el Arte de la Limpieza de Datos en Big Data

https://www.youtube.com/watch?v=fpF-GJn4kXk

---

Curso COMPLETO de IA desde Cero (con PYTHON)!! : Limpieza de datos - Modulo 1


https://www.youtube.com/watch?v=QLKPEOl5oLA


---
Curso COMPLETO de IA desde Cero (con PYTHON)!! : Limpieza de datos (PARTE 2) - Modulo 1

https://www.youtube.com/watch?v=QTn-H3b9lg0


---
Tutorial: ¡SCIKIT-LEARN DESDE CERO!

https://www.youtube.com/watch?v=qUjIybMkXBs

Codificando Bits

---
Tutorial: ¿cómo ALMACENAR Y LEER un modelo en Scikit-Learn?

https://www.youtube.com/watch?v=jrECkCRpU4s

Codificando Bits

---
Tutorial: AFINACIÓN DE HIPER-PARÁMETROS en Scikit-Learn

https://www.youtube.com/watch?v=hcbVLNZ2gAQ

Codificando Bits

---
¿Cómo manejar un dataset DESBALANCEADO en Machine Learning?

https://www.youtube.com/watch?v=8CE4I8o4ZM0

Codificando Bits
---

¿Cómo manejar los VALORES EXTREMOS en nuestros datos?

https://www.youtube.com/watch?v=GiX51cG-tO4

Codificando Bits

---
¿Cómo manejar los DATOS FALTANTES?: guía completa


https://www.youtube.com/watch?v=ARwHkq4t2q0

Codificando Bits

---

Tutorial: MANEJO DE DATOS CATEGÓRICOS FALTANTES con Python, Pandas y Scikit-Learn

https://www.youtube.com/watch?v=G3tNCSQUoXw

Codificando Bits

---

Los sets de entrenamiento, validación y prueba

https://www.youtube.com/watch?v=79K93XBOsIg

Codificando Bits

---
Clasificación con Árboles de Decisión ¡EN 15 MINUTOS!

https://www.youtube.com/watch?v=kqaLlte6P6o


Codificando Bits

---
Regresión con Árboles de Decisión: el algoritmo CART

https://www.youtube.com/watch?v=2Miw4bjzSF0


Codificando Bits

---

La Matriz de Confusión

https://www.youtube.com/watch?v=haEWWO0b42Y


datos balanceados y desbalanceados



Codificando Bits

---

PRECISION, RECALL Y F-SCORE: ¿qué son y cuándo usarlos?

https://www.youtube.com/watch?v=H8FSfqxRWmA

relacionado con la exactitud de un modelos y la matriz de Confusion, mas metricas porque la matriz de confusion no es suficiente para medir la precision(accuracy) o exactitud de los modelos

tambien relacionado con set de datos desbalanceados

Codificando Bits

---




---