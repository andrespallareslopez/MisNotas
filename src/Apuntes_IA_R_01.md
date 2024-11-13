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