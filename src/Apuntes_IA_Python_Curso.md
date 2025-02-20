# Apuntes Python Curso - Bloque 2: Analisis predictivo

# Prediccion de valores numericos

## Regresion lineal

## Arboles de decision

DT (Decision Trees)

-Arboles de Regresion

-Arboles de clasificacion

cada nodo de decision

Impureza de los nodos hojas MSE(Mean Squared Error) error cuadratico medio

RMSE(Root-Mean squared Error)

Poda de un DT (Decision Trees)

Puede a haber problemas de sobreaprendizaje, sobreajuste o overfitting

## Solucion con arboles de decision

## Evaluacion de los modelos predictivos

### Tecnicas de evaluacion

- Validacion cruzada aleatoria (Kold-out)
- Validacion cruzada con k iteraciones (k-fold)
- Validacion cruzada dejando una muestra fuera(Leave-one-out)


## Introduccion al diseño de redes neuronales

### Neuronas artificiales

### Funciones de activacion

- Sigmoide
- ReLU (funcion rectificador lineal)



### Capas de neuronas

capas ocultas o capas intermedias

### Implementacion de redes neuronales en Python

Tensorflow o keras

### Capa de entrada

### Capa de salida

### Capas ocultas

### Compilacion y ajuste del modelo

### Solucion con redes neuronales

# Clasificacion binaria

clasificar elementos en categorias

- clasificacion binaria
- clasificacion multiclase

## Clasificacion mediante tecnicas de regresion





## Clasificacion mediante tecnicas de agrupamiento

- k-medias


## Introduccion a la maquinas de vectores de soporte

- maquinas de vectores

## Caracteristicas basicas de las SVM


## Busqueda de separabilidad en dimensiones superiores


kernel trick

## Ajuste de parametros con busqueda en cuadricula


## Evaluacion del rendimiento predictivo de un clasificador (I)

- matriz de confusion

- Exactitud, precision y sensibilidad(TPR)

### Equilibrio entre precision y sensibilidad


### Otras metricas obtenidas de la matriz de confusion

- Especifidad
- False Positive Rate(FPR)
- Kappa

## Entrenamiento de redes neuronales

# BLOQUE 3 - Analisis descriptivo

- Agrupamiento de datos
- Sistemas de recomendacion

## Agrupamiento de datos

Enfoque no aprendizaje no supervisado

El agrupamiento de datos tambien se le donomina *clustering*.

Tecnicas de agrupamiento:
- Partitivo
- Jerarquico
- Densidad

## Como medir la distancia entre dos muestras

- Distancia euclidea
- Distancia Manhattan
- Distancia del maximo

Generalizacion: distancias de Minkowski, incorpora las otras tres tipos de distancia.

Para p=1 distancia de Manhattan.
Para p=2 distancia euclidea
Para valores p grandes, tiende a infinito, se parecera a la distancia del maximo.

## Agrupamiento por particionamiento - k -medias

kmeans(...) devuelve una estructura como la siguiente:

-cluster: un vector que indica el grupo al que se ha asignado cada una de las muestras del conjunto de datos
-centers:una matriz con k filas, una por grupo, y tantas columnas como dimensiones (variables) haya en el conjunto de datos, indicando el centro de cada grupo en el espacio.
-size:número de muestras asignadas a cada uno de los k grupos.
-tot.withinss: suma total de error cuadradico de los k grupos.


## Problemas del algoritmo k-medias

Inconvenientes:

- La necesidad de conocer de antemano el valor de k
- Su comportamiento aleatorio
- El hecho de que los grupos hayan de tener todos una misma forma y aproximadamente el mismo tamaño
- Su sensibilidad a los valores extremos u outliers

## Agrupamiento por densidad en R

-Algoritmo DBSCAN




