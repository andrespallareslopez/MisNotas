# Apuntes R IA machine learning

---
## practicas

que es el comando str?
similar a summary
~~~
spambase <- read.csv("spambase.csv")

# visualizar la estructura interna de un objeto
str(spambase)

# sumarizar o dar un resumen de los datos, en valores de medias, cuartiles, frecuencias,etc...

summary(spambase)


# visualizar de forma tabulada los datos en una de las ventanas de R
view(spambase)

# para limpiar la consola 
shell("cls")

# instala el packete mldr
install.packages("mldr")


~~~


~~~

~~~



----

Leer datos desde el portapapeles

~~~
read.delim("clipboard")


~~~


~~~

spambase <- read.csv(file="spambase.csv")


mnist <- read.arff("mnist-train.arff")
str(mnist)

~~~

~~~

~~~




---
## Seleccionar datos con [] y subset

Trabajando con datasets en R

https://soka.gitlab.io/blog/post/2019-03-15-r-seleecionar-datos-subset/



~~~
iris["Sepal.Width"]
iris$Sepal.Width

iris[c("Sepal.Width","Sepal.Length")]
~~~


~~~
iris[iris$Species=="setosa",]
~~~

~~~
iris1 <- subset(iris,iris$Sepal.Width > 3 & iris$Species == 'setosa')
~~~



~~~
filter(iris,iris$Sepal.Length >3)[1:4]
~~~


~~~
filter(iris,iris$Sepal.Length >3)[c("Sepal.Length","Petal.Length")]
~~~

---
## Estructuras de datos complejos

arrays
matrices
listas
dataframe



---
## Como CREAR un DATAFRAME en R STUDIO 💻📊 #08 [ CURSO R STUDIO ]

https://www.youtube.com/watch?v=BT7LJu2A5_M



~~~

~~~


---
## Tutorial sobre algunas formas de unir DataFrames mediante los comandos rbind() y cbind() en R.

Unir DataFrames. rbind() y cbind()

~~~
DatosTesPeso = read.table("PotatoTestigoPeso.csv", header=T, sep="," , dec=".")
DatosTesNr = read.table("PotatoTestigoNr.csv", header=T, sep="," , dec=".")
DatosTdoPeso = read.table("PotatoTratadoPeso.csv", header=T, sep="," , dec=".")
DatosTdoNr = read.table("PotatoTratadoNr.csv", header=T, sep="," , dec=".")
~~~



~~~
DatosPesos = rbind(DatosTesPeso, DatosTdoPeso)
View (DatosPesos)
~~~


~~~
DatosNumero = rbind(DatosTesNr, DatosTdoNr)
View (DatosNumero)
~~~

~~~
DatosTotal = cbind(DatosPesos, DatosNumero)
View (DatosTotal)
~~~

Observamos que las columnas Tratamiento, Variedad y Parcela se encuentran repetidas. Lo podemos solucionar uniendo sólo las columnas que nos interesan.


~~~
DatosTotal = cbind(DatosPesos, DatosNumero[ , 4:7])
View (DatosTotal)
~~~

---

## Una manera de montar un dataframe

~~~
altura <- c(180,175,190,189,180....)
peso <- c(80,75,85,....)

datos <- data.frame(peso <- peso, altura <- altura)
~~~


de esta manera montamos un dataframe



---
## GGPLOT2 desde cero: Datos y componentes | Tutorial RStudio en Español

https://www.youtube.com/watch?v=O8p4pMb-ezc





---

## Tips, ideas, notas para graficas sacadas de los apuntes del cursos machine learing

los conteos de un conjunto de datos en phyton con value_counts()


---
