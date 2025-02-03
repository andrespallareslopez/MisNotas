# Apuntes Machine Learning 

## The math behind A.I: From Machine Learning to Deep Learning

https://medium.com/@grethermurray.theodore/the-math-behind-a-i-from-machine-learning-to-deep-learning-e2400fd66f20

---
## Machine Learning Algorithms

https://www.geeksforgeeks.org/machine-learning-algorithms/






---

## Machine Learning Algorithms: Mathematical Deep Dive

https://viso.ai/deep-learning/machine-learning-algorithms-mathematical-guide/

---

## Stochastic Dual Coordinate Ascent

https://michaelkarpe.github.io/machine-learning-projects/sdca/


---

## Tutorial 12- Stochastic Gradient Descent vs Gradient Descent

https://www.youtube.com/watch?v=FpDsDn-fBKA



---

## 1.- Redes Neuronales: Fácil y desde cero

https://www.youtube.com/watch?v=jaEIv_E29sk&list=PLAnA8FVrBl8AWkZmbswwWiF8a_52dQ3JQ


- Percectron multicapa



---

## 2.- Redes Neuronales: Fácil y desde cero

https://www.youtube.com/watch?v=rmz1pzfDZUo&list=PLAnA8FVrBl8AWkZmbswwWiF8a_52dQ3JQ&index=2

Descenso del gradiente




---

## 3.- Redes Neuronales: Fácil y desde cero

https://www.youtube.com/watch?v=7igBj20dmlw&list=PLAnA8FVrBl8AWkZmbswwWiF8a_52dQ3JQ&index=3

-capa de entrada
-capa de salida

-capas oculta




---

## 4a.- Redes Neuronales: Fácil y desde cero


Back Propagation


---

## Máquinas de soporte Vectorial


https://www.youtube.com/watch?v=vemcbJnRqJU&t=29s


---

## Database Normalization for Beginners | How to Normalize Data w/ Power Query (full tutorial!)

https://www.youtube.com/watch?v=rcrsqyFtJ_4

---
## CURSO de MACHINE LEARNING desde CERO | (COMPLETO)

https://www.youtube.com/watch?v=xyU2pzKTQE0


Adrian Cancino

### regresion lineal simple

~~~
import pandas as pd
import matplotlib.pyplot as plt

data = data.read_csv('.....')

data = data.iloc[:,1:]
data.head()
data.info()

data.describe()

data.columns


cols = ['TV','Radio','Newspaper']
for col in cols:
   plt.plot(data[col],data['sales],'ro')
   plt.title('Ventas respecto a la publicidad en %s',col)
   plt.show()

from sklearn.linear_model import LinearRegresion
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error,r2_score

X = data['TV'].values.reshape(-1,1)
X
Y =data['sales'].values
# dividir el conjunto de datos entre entrenamiento y testing

X_train,X_test,y_train,y_test = train_test_split(X,y,test_size=0.2,random_state=42)

print(X_train.shape)
print(X_test.shape)

lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)

y_pred = lin_reg.predict(X_test)

print('Predicciones:{}, REales'.format(y_pred[:4],y_test[:4]))

#RMSE
rmse = mean_squared_error(y_test,y_pred,squared=false)
print('RMSE',rmse)
#R2
print('R2;',r2_score(y_test_y_pred))

plt.plot(X_test,y_test,'ro')
plt.plot(X_test,y_pred)
plt.show()





~~~





### regresion lineal multiple
~~~








~~~

### modelos de regresion polinomica
~~~





~~~

### Maquinar de soporte vetorial para regresion SVR

~~~
# la maquina de soporte vectorial nos sirve con datos complejos
# que este no es el caso, pero lo podemos aplicar, nos podemos quedar
# con la regresion multiple




data = data.read_csv('content/sample_data/Adversiting.csv')

data = data.iloc[:, 1:]

import sklearn.svm import SVR

from sklearn.model_selection import train_test_split
from sklearn.metrics import r2_score

# TV - NewsPaper
X = data.drop(['Radio','Sales'],axis=1).values
y = data['sales'].values

X_train,X_test,y_train,y_test = train_test_split(X,y,test_size=0.2,random_state=42)

# Si miramos la documentacion de SRV del kernel viene varios modelos
srv = SRV(kernel='lineal')
svr.fit(X_train,y_train)

y_pred = svr.predict(X_test)
print('Reales:',y_test[:4],'Prediccion:',y_pred[:4])

r2_score(y_test,y_pred)

# variables TV - Radio

X = data.drop(['Newspaper','Sales'],axis=1).values
y = data['Sales'].values

X_train, X_test,Y_test = train_test_split(X,y,test_size=0.2,random_state=42)

svr = SVR(kernel='rbf')
svr.fit(X_train,y_train)ç


y_pred =svr.predict(X_test)
r2_score(y_test,y_pred)






~~~



### California (Exploracion conjunto de datos)
~~~




#grafico para ver la correlacion
sns.heatmap(data.corr(),annot=True)

# para ver la correlacion entre variables

corr_matrix= data.corr()




x = [1,2,3,np.nan]
x1= pd.Series(x)

x1.mean()
~~~

Limpieza de datos manejar atributos categoricos


~~~
# quitar los nulos o lo not avaiable
data['total bedrooms'].fillna(data['total bedroosm'].median(),inplace=True)

from sklearn.preprocesing import OrdinalEncoder

data_ocean = data[['ocean_proximity']]
ordinal_encoder = OrdinalEncoder()
data_ocean_encoded = ordinal_encoder.fit_transform(data_ocean)

# OneHotEncoder
import sklearn.reprocesing import OneHotEncoder
cat_encoder = OneHotEncoder()
data_car_1hot = cat_encoder.fit_transform(data_ocean)
data_cat_1hot.toarray()


encoded_df = pd.DataFrame(data_cat_1hot.toarray(),columns=cat_encoder.get_feature_names_out())
encoded_df.head()



~~~

### Crear los algoritmos de machine learning

~~~

y = data['median_house_value'].values.reshape(-1,1)

X = data[['median_income','rooms_per_household','total_rooms','housing_median_age','households']]

data1 = pd.concat([X,encoded_df],axis=1)  # axis=1 concatenar por columna
data1.columns


~~~

### Regresion Lineal multiple

~~~
from sklearn.model_selection import train_test_split

X_train,X_test,y_train,y_test = train_test_split(x,y,test_size=0.2)


print(X_train.shape)
pring(y_train)


~~~

### Escalar variables


~~~


from sklearn.preprocesing import StandardScaler

SC_X = StandardScaler()

X = sc_X.fit_transform(X)




~~~


### Analisis de las variables cuales son las mejores - California house Price


~~~
columnas =['median_income','rooms_per_household','total_rooms','housing_median_age','households','latitude','longitude']

col_modelo = []

y = data['median_hous_value'].values.reshape(-1,1)

for col in columnas:
   col_modelo.append(col)
   data1 = data[col_modelo]
   data1 = pd.concat([data1,encoded_df],axis=1)
   x = data1.values


X_train,X_test,y_train,y_test = train_test_split( X,y,test_size=0.2 )
lin_reg = LinearRegression()
lin_reg.fit(X_train,y_train)
y_pred = lin_ref.predict(X_test)
r2 = r2_score(y_test,y_pred)
pring(col_modelo,r2)





~~~

### Arboles de decision y bosques aleatorios


### Arbol de decision
~~~

from sklearn.tree import DecisionTreeRegressor

columnas =['median_income','rooms_per_household','total_rooms','housing_median_age','households','latitude','longitude']

col_modelo = []

y = data['median_hous_value'].values.reshape(-1,1)

for col in columnas:
   col_modelo.append(col)
   data1 = data[col_modelo]
   data1 = pd.concat([data1,encoded_df],axis=1)
   x = data1.values


X_train,X_test,y_train,y_test = train_test_split( X,y,test_size=0.2 )
lin_reg = DecisionTreeRegressor()
lin_reg.fit(X_train,y_train)
y_pred = lin_ref.predict(X_test)
r2 = r2_score(y_test,y_pred)
pring(col_modelo,r2)


~~~


### Bosque aleatorio
~~~


from sklearn.tree import RandomForestRegressor

columnas =['median_income','rooms_per_household','total_rooms','housing_median_age','households','latitude','longitude']

col_modelo = []

y = data['median_hous_value'].values.reshape(-1,1)

for col in columnas:
   col_modelo.append(col)
   data1 = data[col_modelo]
   data1 = pd.concat([data1,encoded_df],axis=1)
   x = data1.values


X_train,X_test,y_train,y_test = train_test_split( X,y,test_size=0.2 )
lin_reg = RandomForestRegressor()
lin_reg.fit(X_train,y_train)
y_pred = lin_ref.predict(X_test)
r2 = r2_score(y_test,y_pred)
pring(col_modelo,r2)


~~~

### Algoritmos de clasificacion

### problema Mnist es visual numero escritos a mano por personas, clasificar imagenes
~~~

import numpy as np
import matplotlib.pyplot as plt

import sklearn.datasets import fetch_openml

mnist = fetch_openml('mnist_784',version-1)

#pre analisis exploratorio

mnist.keys()

x, y = mnist['data'], mnist['target']   # ¿? repasar target que es

print(x.shape)
print(y.shape)

#cada imagen 28x28 pixeles
# escala de grises o blanco - negro

digit = X.to_numpy()[0]
digit_image = digit.reshape(28,28)

plt.imshow(digit_image, cmap='binary')
plt.show()

# nos muestra una imagen de 5

y = y.astype(np.uint8)
y[0]

# nos dice el numero 5

X_train,X_test, y_train , y_test = X[:60000],X[60000:],y[:60000],y[60000:]

# solo cogemos el numero de 5 que son la imagen 5

y_train_5 = (y_train == 5)
y_test_5 = (y_test == 5)

from sklearn.linear_model import SGDCClassifier
sgd_classifier = SGDClassifier(random_state=42)
sgd_classifer.fit(X_train,y_train_5)


sgd_classifier.predict([digit])

# medir el rendimiento del modelo

from sklearn.model_selection import cross_val_score

cross_val_score(sgd_classifier,X_train,y_train_5,cv=3,scoring='accuracy')




~~~

### otra manera de medir el rendimiento o fiabilidad del modelo

### La matriz de confusion

TN : valores nuestro algoritmos que no eran numero 5 y estaba en lo correcto verdaderos negativos
FP : falsos positivos algoritmos dijo eran 5 y se equivoco
FN : Falsos negativos      ''    dijo no eran 5 y se equivoco
TP : Verdaderos positivos, '' si era el numero 5 y era correcto 

|||
|--|--|
|TN|FP|
|FN|TP|



~~~
from sklearn.model_selection import coss_val_predic

y_train_pred = cross_val_predict(sgd_classifier, X_train,y_train_5,cv=3)


~~~


### Regresion Logistica

~~~
import pandas as pd
import numpy as np

data = pd.read_csv(/content/sample_data/Social_Network_ads.csv)
data.head()


x = data.iloc[;,[2,3]]
y = data.iloc[:,-1].values

from sklearn.preprocesing import OneHotEncoder

gender = data[['Gender']]

cat_encoder = OneHotEncoder()
data_cat_1hot = cat_endoder.fit_transformer(gender)

cat_encoder.categories_

data_cat_1hot.toarray(:3)

encoded_df = pd.DataFrame(date_cat_1hot.toaaray(), columns = cat_encoder.get_feature_names_out())

encoded_df.head()

data1 = pd.concat([X,encoded_df],axis=1)
data1.head()

from sklearn.model_selection import train_test_split
X_train,X_test,y_train,y_test = train_test_split(data1,y,test_size=0.2,random_state=0)

print(X_train.shape)
print(X_test.shape)


from sklearn.preprocesing import StandardScaler

sc_X = StandarScaler()

X_train = sc_X.fit_transform(X_train)

X_test = sc_X.fit_trasform(X_test)

from sklearn.linear_model import LogisticRegression

log_reg = LogisticRegression(random_state=0)
log_reg.fit(X_train,y_train)

y_pred = log_reg.predict(X_test)

print ('Reales:',y_test[:10], 'Prediction:',y_pred[:10])

from sklearn.metrics import confusion_matrix

confusion_matrix(y_test,y_pred)

from sklearn.metrics import precision_score,f1_score

print('Precision',precision_score(y_test,y_pred))
print('Memoria',recall_score(y_test,y_pred))
print('F1_score',f1_score(y_test,y_pred))




~~~

### K-NN

~~~

# distancia
# Euclidiana
# Manhattan
# Minkowski

# algoritmo para muchos datos no es tan eficiente

data = pd.read_csv('/content/sample_Data/Social_Network_Ads.csv')
data.head()
X = data.iloc[: [2,3]]
y = data.ilog[:,-1].values

gender = data[['gender']]
from sklearn.preprocesing import OnHotEncoder
cat_encoder = OneHotEncoder()
data_cat_1hot = cat_encoder.fit_transform(gender)

encoded_df = pd.DataFrame(data_cat_1hot.toarray(),columns=cat_encoder.get_feature_names_out())

encoded_df.head()

data1= pd.concat([X,encoded_df],axis=1)
data1.head()

from sklearn.model_selection import train_test_split
X_train,X_test,y_train,y_test = train_test_split(data1,y,test_size=0.2,random_state=0)

from sklearn.preprocesing import StandardScaler
sc_X = StandardScaler()
X_train = sc_X.fit_transform(X_train)
X_test = sc_X.transform(X_test)

from sklearn.neigbors import KneighborsClassifier
knn= KneigborsClassifier(metric='minkowski',p=1)
knn.fit(X_train,y_train)

y_pred = knn.predict(X_test)

print('Reales:',y_test[:10],'Prediccion',y_pred)

from sklearn.metrics import confusion_matrix
confusion_matrix(y_test,y_pred)

from sklearn.metrics import precision_score,recall_score,f1_score

print('Precision',precision_score(y_test,y_pred))
print('Memoria',recall_score(y_test,y_pred))
print('F1_score',f1_score(y_test,y_pred))




~~~


### Maquinas de soporte vectorial para clasificacion SVC

~~~

# hacemos lo mismo que la anterior con el KNN






data = pd.read_csv('/content/sample_Data/Social_Network_Ads.csv')
data.head()
X = data.iloc[: [2,3]]
y = data.ilog[:,-1].values

gender = data[['gender']]
from sklearn.preprocesing import OnHotEncoder
cat_encoder = OneHotEncoder()
data_cat_1hot = cat_encoder.fit_transform(gender)

encoded_df = pd.DataFrame(data_cat_1hot.toarray(),columns=cat_encoder.get_feature_names_out())

encoded_df.head()

data1= pd.concat([X,encoded_df],axis=1)
data1.head()

from sklearn.model_selection import train_test_split
X_train,X_test,y_train,y_test = train_test_split(data1,y,test_size=0.2,random_state=0)

from sklearn.preprocesing import StandardScaler
sc_X = StandardScaler()
X_train = sc_X.fit_transform(X_train)
X_test = sc_X.transform(X_test)

from sklearn.svm import SVC

cls = SVC(Kernel='linear',random_state=0)
cls.fit(X_train,y_train)

y_pred = cls.predict(X_test)

from sklearn.metrics import confucion_matrix

print(confusion_matrix(y_test,y_pred))

from sklearn.metrics import precision_score,recall_score
print('Precision',precision_score(y_test,y_pred))
print('Recall', recall_score(y_test,y_pred))

from sklearn.metrics import f1_score

print('F1:',f1_score(y_test,y_pred))




~~~


---

## Aprende PANDAS y MATPLOTLIB desde cero

https://www.youtube.com/watch?v=-owci852QSE&list=PL7L9BEVTY9bODO9czTp3VhahlO_nAkajh

Adrian Cancino

~~~

import pandas as pd
import matplotlib.pyplot as plt

# crear un conjunto de datos dataframe

year = [2012,2013,2014,2015]

calificaciones = [100,96,75,30]

cal_dict = ['years':years,'calificaciones': calificaciones]

print(calc_dict)

cal_df = pd.DataFrame(calc_dict)

calc_df.head()


# por defecto grafico de lineas
plt.plot('years','calificaciones',data=calc_df)
# a posteriori podemos poner un titulo y otras caracteristicas
plt.title('Calificaciones a lo largo de los años')

plt.xlabel('Años')
plt.ylabel('calificaciones')


plt.show()

# conjunto de datos mas grande

# carga informacion en base a un conjunto de datos

netfilx_df = pd.read_csv('/content/sample_data/netflix_data.csv')
# primeras 5 filas
netflix_df.head()

# ultimas 5 filas
netfilx_df.tail()

# para saber las dimensiones del dataframe
netflix_df.shape

# pueden aparecer columnas donde el numero de filas no coincide y faltan datos, con este metodo se ve
netflix_df.info()

# resumen de las columnas numericas, resumen de varios valores estadisticos de las columnas numericas

netflix_df.describe()

# comenzamos con el analisis

# me devuelve una columna, tenemos la columna 'type' para el dataframe 

netflix_df.type
#otra forma
netflix_df[['type','duration']]

# valores unicos de esta columna
netfilx_df['type'].unique()

# filtrado de los datos

netflix_df_movies = netflix_df[netflix_df['type'] == 'Movie']

# quedarme con las columnas que yo quiero de un dataframe, que se muestre en otro dataframe a partir de otro

netflix_df_movies_columns = netflix_df_movies[['title','country','genre','release_year','duration']]

# crear un grafico de puntos


# cambiar el tamaño del grafico
fig = plt.figure(figsize=(12,8))

plt.scatter('release_year','duracion',data=netflix_df_movies_columns)
# me falta poner informacion adicional para que el grafico se entienda
plt.title('duracion de las peliculas a lo largo de los años')
plt.xlabel('años')
plt.ylabel('minutos')

plt.show()

# ahora se dibuja de mejor forma

# vamos a ver los maximos y los minimos, puntos atipicos de un rango muy alto o muy bajo

# obtener el valor mas pequeño de una columna, obtenemos la pelicula con menos duracion y mayor duracion
netflix_df_movies_columns.nsmallest(n=1,columns='duration')

netflix_df_movies_columns.nlargest(n=1,columns='duration')

# para saber el conteo de una columna, las frecuencias de la columna por genero

netflix_df_movies_columns['genre'].value_counts()

# filtrado multiple utilizando tuberias

netflix_df_movies_filtered = netflix_df_columns[
   (netflix_df_movies_columns['genre'] == 'Dramas') |
   (netflix_df_movies_columns['genre'] == 'Comedies') |
   (netflix_df_movies_columns['genre'] == 'Documentaries')
   
]

colors = []

for lab,row in netflix_df_movies_filtered.iterrows():
   print(lab)
   print(row)
   break   # solo me da la primera fila

for lab,row in netflix_df_movies_filtered.iterrows():
   if row['genre'] == 'Drames':
       colors.append('red')
   elif row['genre'] == 'Documentaries':
       colors.append('blue')
   else:
       colors.append('black')

print(colors[:10])

plt.style.use('fivethirtyeight')  # se agregaria una cuadricula al grafico
fig = plt.figure(figsize=(12,8))

plt.scatter('release_year','duration', data=netflix_df_movies_filtered,color=colors)
plt.title('Duracion de las peliculas a lo largo de los años')
plt.xlabel('años')
plt.ylabel('Minutos')

plt.show()

# ahora vamos a ver como crear un grafico de barras en case a un conteo

plt.style.use('fivethirtyeight')  # se agregaria una cuadricula al grafico
fig = plt.figure(figsize=(12,8))

count_movies = netflix_df_movies_columns['genre'].value_counts()

# obtener el indice y los valores por separa en value_counts()

ptl.bar(count_movies.index,count_movies.values)

# las etiquetas se ven mal, y la barra no es suficiente ancho
# voy a rotar las etiquetas en el ejex
plt.xticks(rotation=90)
plt.title('Cantidad de peliculas por genero')
plt.xlabel('generos')
plt.ylabel('cantidad)


plt.show()

# el muestreo de la duracion de las peliculas de este conjunto de datos

# el promedio de la duracion de las peliculas a lo largo de los años

# agrupar los datos por año

# nos va a mostrar una lista, si no le ponemos el reset_index() se pone como una serie
movies_duration_year = netfilx_df_movies_columns.groupby('release_year')['duration'].mean().reset_index()  # se acerca como un dataframe


plt.style.use('fivethirtyeight')  # se agregaria una cuadricula al grafico
fig = plt.figure(figsize=(12,8))

plt.plot('release_year','duration',data=movies_duration_year)
plt.title('duracion de las peliculas por año')
plt.xlabel('año')
plt.ylabel('duracion promedio')

plt.show()


# conteo de las peliculas que mas y menos tienen por paises. cojo los 10 primeros paises

count_countries = netflix_df_movies_columns['country'].value_counts().head(10)

# grafico de barrar horizontal


plt.style.use('fivethirtyeight')  # se agregaria una cuadricula al grafico
fig = plt.figure(figsize=(12,8))


plt.barh(count_countries.index,count_countries.values)
plt.title('cantidad de peliculas por pais')

plt.show()












~~~




---
## Reshape -1, 1 and Reshape 1, -1 in Python NumPy | Module NumPy Tutorial - Part 07

https://www.youtube.com/watch?v=yDXNPyxDb0M





---




---