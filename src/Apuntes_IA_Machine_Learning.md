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

 regresionn lineal simple
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



regresion lineal multiple
~~~





~~~

modelos de regresion polinomica
~~~





~~~

California (Exploracion conjunto de datos)
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

Crear los algoritmos de machine learning

~~~

y = data['median_house_value'].values.reshape(-1,1)

X = data[['median_income','rooms_per_household','total_rooms','housing_median_age','households']]

data1 = pd.concat([X,encoded_df],axis=1)  # axis=1 concatenar por columna
data1.columns


~~~

Regresion Lineal multiple

~~~
from sklearn.model_selection import train_test_split

X_train,X_test,y_train,y_test = train_test_split(x,y,test_size=0.2)

print(X_train.shape)
pring(y_train)
~~~

Escalar variables


~~~


from sklearn.preprocesing import StandardScaler

SC_X = StandardScaler()

X = sc_X.fit_transform(X)




~~~


Analisis de las variables cuales son las mejores - California house Price


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

Arboles de decision y bosques aleatorios


Arbol de decision
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


Bosque aleatorio
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

Algoritmos de clasificacion

problema Mnist es visual numero escritos a mano por personas, clasificar imagenes
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

otra manera de medir el rendimiento o fiabilidad del modelo

La matriz de confusion

TN : valores nuestro algoritmos que no eran numero 5 y estaba en lo correcto verdaderos negativos
FP : falsos positivos algoritmos dijo eran 5 y se equivoco
FN : Falsos negativos      ''    dijo no eran 5 y se equivoco
TP : Verdaderos positivos, ''si era el numero 5 y era correcto 

|||
|--|--|
|TN|FP|
|FN|TP|






---


