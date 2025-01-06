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

## Leer datos desde el portapapeles

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



---
## Resumen curso machine learning R

Crear un dataframe desde cero, con varios vectores o listas¿?:



### Carga de datos desde diferentes fuentes:

podemos cargar para csv:
~~~
read.csv()
read.csv2()
read.delim()
read.table()
~~~
podemos cargar arff:

~~~
library(foreign)
read.arff(file="...")

~~~

podemos cargar excel:
~~~
library("xlsx")
read.xlsx(file='...')
~~~
podemos cargar en el clipboard:

~~~
read.delim("clipboard")

~~~

podemos cargar desde una url:

~~~
spambase.url <-"https://....."

spambase <- read.csv(spambase.url)


~~~

podemos cargar datos de webscraping:
 
 instalar paquete rvest

Exportacion de datos

Exportacion a formatos de texto

csv, arff

exportacion csv

~~~
write.csv(datos,"nombrearchivo")
write.csv2(datos,"nombrearchivo")

~~~

exportacion arff

~~~
library(foreign)

write.arff(datos,"nombrearchivo.arff")

~~~

### Exportacion a formatos binarios propios de r

~~~
saveRDS(datos,file="nombrefichero.Rds")
save(datos,file = "datos.Rda")

datos <- readRDS("Datos.rds")

datos <- load("datos.Rda")

~~~

### Trabajar con archivos HDF5 desde R

~~~
 install.packages("BiocManager")
 BiocManager::install("rhdf5")


> library(rhdf5)
>
> archivoH5 <- "Modulo2.h5"
>
> h5createFile(archivoH5)
>
> h5createGroup(archivoH5, "DatosMedicos")
> h5write(read.csv("Limpieza.csv"), archivoH5, "DatosMedicos/Originales")
> h5write(datos.limpios, archivoH5, "DatosMedicos/Limpios")

~~~

### Analisis exploratorio de datos

~~~
> datos <- read.csv("Limpieza.csv", stringsAsFactors = TRUE)

~~~


### Limpieza de Datos







---

## Factores en R

https://www.youtube.com/watch?v=ZLCFD3b6kTg

---

## Introducción a R. Ejemplo exploración de datos

https://www.youtube.com/watch?v=P1FQCEPcWwo&list=PL6kQim6ljTJthrG_GLZxrPeuR7qQfEKgv&index=35



---
## Data.frame en R

https://www.youtube.com/watch?v=uQKkydX4tP4&list=PL6kQim6ljTJthrG_GLZxrPeuR7qQfEKgv&index=23

Filtros, ejemplos:
~~~

d2[d2$ciudad=="Valencia",c("nombre","edad")]

#saca todas las columas con edad >35
d2[d2$edad>35,]
~~~


---
## Otros Objetos en R: Vectores y Matrices

https://www.youtube.com/watch?v=-176Z8LyOe8


---

## Variables categóricas en R: Uso función factor

https://www.youtube.com/watch?v=8tsMqkyBfp0





---
## Lenguaje R. Introducción a los gráficos con ggplot() | 31/41 | UPV

https://www.youtube.com/watch?v=S3WH0NytcLo&list=PL6kQim6ljTJthrG_GLZxrPeuR7qQfEKgv&index=31

Datos + Estetica + Capas + Facetas()

~~~
library(ggplot2)

p<- ggplot(iris)
p
p <- p + aes(x=Petal.Length,y=Petal.Width, colour=Species)
p
p<- p + geom_point()
p
p<-p + geom_smooth()
p<-p + facet_grid(~ Species)
p





~~~


---
##  La función melt y datos en formato largo

https://luisxsuper.github.io/bibroxd/la-funcion-melt-y-datos-en-formato-largo.html




---
## MODELOS estadísticos en R 💻 Ejemplo de REGRESION Lineal Simple

https://aulas.campusmvp.com/SELF/lesson.self?LessonId=113787




---

## Arboles de decision | Creación, Precisión y Predicción con Valores Nuevos

https://www.youtube.com/watch?v=FyAOTkCXtzM




---
## Clasificación con Árboles de Decisión ¡EN 15 MINUTOS!

https://www.youtube.com/watch?v=kqaLlte6P6o

---

## Regresión con Árboles de Decisión: el algoritmo CART

https://www.youtube.com/watch?v=2Miw4bjzSF0




---

## 1 | Árboles de Decisión en R: Árbol de Clasificación |


https://www.youtube.com/watch?v=tDeIo43pHGg&t=1262s



---

¿Cómo funciona SVM?

https://www.youtube.com/watch?v=kl6tyEi5eso
---

MÁQUINAS DE SOPORTE VECTORIAL: ¡explicación COMPLETA!

https://www.youtube.com/watch?v=Xbd8T-JoGPQ

---




---