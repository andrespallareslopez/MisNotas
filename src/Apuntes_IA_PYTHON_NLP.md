# Apuntes procesamiento de lenguaje natural

---
## Curso Completo de Procesamiento de Lenguaje Natural (NLP) con Python

https://www.youtube.com/watch?v=9x1QtYNLJRY

Codigo espinoza


## bolsa de palabras

-El orden de las palabras

## metodo de conteo
las ocurrencias o frecuencia con que aparecen cada palabra en el texto o secuencia de palabras.

## Tokenizacion
dividir el texto en tokens
los tokens son las unidades individuales de un texto

Tokenizacion basada en palabras
       ''    basada en caracteres
basada en sub-palabras(automivil -> auto, movil)

Diferentes casos de letras(tildes por ejemplo)
Tokenizar por palabras completas, caracteres o sub-palabras
Puntuacion( tener en cuenta puntos o comas o otros signos como exclamacion,interrogacion)

Manejo de los casos de las letras (mayusculas y minusculas)




-Mapeo

## Stop words o palabras de parada

~~~
import nltk
from nltk.corpus import stopwors
from nltk.tokenize import word_tokenize
nltk.download('stopwords')

stop_words = set(stopworsd.worsd('spanish'))
print(stop_words)

texto= "El gato es negro y el perro es blanco"
texto = texto.lower()

tokens = word_tokenize(texto)
print(tokens)

texto_filtrado = [word for word in tokens if not word in stop_words]

print(texto_filtrado)






~~~


## STEMMING Y LEMMATIZATION

Probelams de la tokenizacion basica y recuento

Las palabras similares se tratan como entidades separadas.
El alto dimensional de los vectores resultantes.
Aplicaciones practivas y desventajas de la tokenizacion basica.

El Stemming es una tecnica mas simple que simplemente elimina los sufijos de las palabras.
La lemmatization es una tecnica mas sotisficada que utiliza las reglas del lenguaje para obtener la base o raiz de una palabra.


~~~
import nltk

nltk.download('wordnet')

from nltk.stem import SnowballStemmer

stemmer = SnowballStemmer('spanish')

print(stemmer.stem('caminando'))
print(stemmer.stem('caminar'))
print(stemmer.stem('camino'))

pip install spacy -q

import spacy

nlp=spacy.load("es_core_news_sm")

nlp = nlp("caminar caminando camino")

for token in doc:
   print(token.text,"->",token.lemma_)






~~~

- Particularidades de la Lemmatization y recomendaciones para su uso
La lemmatization puede ser mas efectiva que el stemming, pero tambien es mas costosa computacionalmente
El uso de la lemmatization puede requerir el etiquetado previo.

- Aplicacion de Stemming y Lemmatization en situaciones reales

Asistentes virtuales y Chatbos.
Analisis de sentimientos.
Motores de busqueda.
Sistemas de recomendacion.
Aplicacion en publicidad online y etiquetas de redes sociales.

- Ejemplo practico


~~~


~~~


~~~


~~~

## Similitud de vectores

Similitud de documentos.
Spinning de articulos y SEO. (spining) variar el articulo, y que diga lo mismo con otras palabras
Recomendaciones.
Chat bots.

- Calcular Similitud de Vectores

Distancia Euclidiana

Angulo entre vectores. Distancia coseno

En el procesamiento del Lenguaje Natural, a menudo se prefiere la similitud del coseno porque toma en cuenta el angulo entre los vectores, que pueden ser mas relevante en contextos donde los vectores representan textos o palabras.

##  Metodo TF-IDF

LA frecuencia del termino Term frecuency (TF), frecuencia inversa del documento IDF

Problemas con el metodo conteo:

No toma en cuenta la relevancia de las palabras.
TF-IDF reduce el peso de las palabras comunes y aumenta el peso de las palabras que no se utilizan con frecuencia.

Stop Words

Palabras comunes como si, la, el mas,etc.
Si se dejan en el texto, pueden sesgar el analisis hacia las palabras mas comunes.
Eliminar las stop words puede hacer que los algoritmos sean mas precisos y rapidos, ya que hay menos palabras a procesar.

Ambiguedad y especificidad de las stop words dependiendo de la aplicacion.

No todas las palabras comunes son stop words en todas las situaciones

Por ejemplo, "no" podria ser una stop word en muchos contextos, pero no en el analisis de sentimientos, donde podria ser una palabra clave.

Descripcion de como funciona TF-IDF

TF-IDF funciona al asignar un puntaje a cada palabra en un documento en funcion de su frecuencia en ese documento (TF) y su frecuencia en todos los documentos (IDF).

Cuanto mas a menudo aparece una palabra en un solo documento, pero menos a menudo en todos los documentos, mayor es su puntaje TF-IDF.

Las palabras que aparecen con mas frecuencia en un documento pero raramentente en otros documento son mas importantes.

-Formulacion de TF-IDF y su justificacion

TF-IDF se calcula multiplicando dos componentes: TF e IDF.

TF se calcula como el numero de veces que aparece una palabra en un documento dividido por el total de palabras en ese documento

IDF se calcula como el logaritmo del total de documentos dividido por el numero de documentos que contienen la palabra

TF-IDF = TF(t,d)*IDF(t,D)

TF(t,d)= (Numero de veces que el termino t aparece en el documento d)/(Total de terminos en el documento d)

IDF(t,D)=log_e(total de documentos en el corpus D / Numero de documentos donde el termino t aparece)

## Aplicacion TF-IDF. Recomendacion de peliculas


~~~
import pandas as pd
dt = pd.read_csv('movie_metadata.csv')

df['genero'] = df['genero'].str.replace('|',' ')

df['plot_keywords'] = df['plot_keywords'].str.replace('|',' ')

df['Texto']= df[['genero','plot_keywords']].apply(lambda row: ' '.join(row.values.astype(srt)),axis=1)

row = df[['genero','plot_keywords','texto']].iloc[0]
print(row)

from sklearn.feature_extraction.text import TfidFVectorizer
from sklearn.metrics.pairwise import cosine_similarity,euclidean_distances

tfidf = TfidfVectorizere(max_features=2000)

X= tfidf.fit_transform(df['texto])

peliculas = pd.Series(df.index,index=df['movie_title'])

peliculas.index = peliculas.index.str.strip()

indice = peliculas['The Dark Knight Rises']

consulta = X[indice]

similitud = cosine_similiraty(consulta,X)

similitud = similitud.flatten()

import matplotlib.pyplot as plt

plt.plot(similitud)

(-similitud).argsort() # orden descendente



~~~


## Neural word embedings

Antes podiamos hacer por bolsa de palabras
Ejemplo de bolsa de palabras

pero podemos convertir las palabras en vectores.

- Metodos de vectorizacion

Conversion de documentos en vectores(Bolsa de palabreas,TF-IDF).
Palabras a vectores.
Descripcion de la representacion de documentos mediante una secuencia de vectores(Embeddings).

-Modelos para secuencias en aprendizaje profundo

Modelos construidos para secuencias (CNN,RNN,Transformes). CNN -> clasificacion positiva o negativa reseñas
Relevancia del orden de las palabras en una sentencia.
Aplicaciones en traduccion de idiomas, respuestas a preguntas, chat bots, y mas.

-Incrustaciones de palabras (World embeddings)

Introduccion a Word2Vec y Glove
Uso de redes neuronales en Word2Vec
    Continuous Bag of Words (CBOW) y Skip-Gram

Descripcion de Glove y su relacion con los sistemas de recomendacion

Descripcion general del proceso de formacion de una red neuronal

- Uso practivo de Word embeddings.

Comparacion entre las incrustaciones de palabras y otros metodos de vectorizacion.
Descripcion de analogias de palabras con incrustaciones de palabras.


## Ejemplo de Word Embeddings : Analogias

En kaggle hay una data llamada Pre-Trained Word Vectors for spanish ocupa 1GB 
SW-vectors-300-min5.txt

Data que ya esta entrenada

~~~
!pip install gensim -q


import gensim

vectores = gensim.models.keydVectors.load_word2vec_format('SW-vectors-300-min5.txt')

def analogias(v1,v2,v3):
    similitud = vectores.most_similar(positive=[v1,v3],negative=[v2])
    print(f"{v1} es a {v2} como {similitud[0][0]} es a {v3}")

analogias('rey','hombre','mujer')

analogias('pan','trigo','huevo')


def cercanos(v):
   vecinos = vectores.most_similar(positive=[v])
   print(f"vecinos de : {v}")
   for word,score in vecinos:
      print("\t%s" % word)


cercanos('rey')


cercanos('Chile')
#diferencia entre mayusculas y minusculas
cercanos('chile')



~~~

https://www.kaggle.com/datasets/rtatman/pretrained-word-vectors-for-spanish


## Crear tus propios Embeddings con word2vec

Word2Vec es un modelo que se utiliza para aprender representaciones vectoriales de palabras. Estas representaciones pueden capturar muchas propiedades linguisticas de las palabras, como su significado semantico y gramaticas y hasta contextual.

~~~
pip install pypdf2 -q

import string
from gensim.models import Word2Vec
import PyPDF2

# carga del documento
with open('Minecraft.txt','r',encoding='utf-8') as file:
    documento = file.read()

len(documento)

# preprocesamiento de datos, vamos a dividir en oraciones, y luego en palabreas

oraciones = documento.split('.')

len(oraciones)

print(oraciones[0])

oraciones_limpias=[]
for oracion in oraciones:
     #Eliminar la puntuacion y dividir por espacios
     tokens = oracion.trasnlate(str.maketrans('','',string.puntuation)).split()
     print(tokens)
     # convertir a minusculas
     tokens = [word.lower() for word in tokends if word.isalpha()]
     if tokens: #Añadir si solo hay tokens
         oraciones_limpias.append(tokens)
     

 print(oraciones_limpia[0])

 # Entrenar el modelo word2vec

 model = Word2Vec(sentences= oraciones_limpias,vector_size=500, windows=5,min_count=1 workders=8)

 vector = model.wv['minecraft']

 palabras_cercanas = model.wv.most_similar("minecraft",topn=10)
 palabras_cercanas

 #guardar el modelo

 model.save('minecraft.model')

 modelo_cargado = Word2Vec.load('minecraft.model')
# guardar solo los embeddings
 model.wv.save_word2vec_format('mine_emb.txt',binary=False)
 model.wv.save_word2vec_format('mine_emb.bin',binary=True)

 # para cargar un embeddings

 from gensim.models import KeyedVectors

 embeddings_cargardos = KeyedVectors.load_word2vec_format('embeddings.txt',binary=False)

def analogias(v1,v2,v3):
    similitud = embeddings_cargados.most_similar(positive=[v1,v3],negative=v2)
    print(f"{v1} es a {v2} como {similitud[0][0]} es a {v3}")




# vamos a entrenar con el libro de 100 años de soledad

def extraer_texto_desde_pdf(ruta_archivo):
      with open(ruta_archivo,'rb') as archivo:
           lector = PyPdf2.PdfReader(archivo)
           texto = ""
           for pagina in range(len(lector.pages)):
               texto += lector.pages[pagina].extract_text()
      return texto

documento = extraer_texto_desde_pdf('100as.pdf')

len(documentos)

# dividir el documento en frases  usando la coma como separador

oraciones = documento.split(',')

len(oraciones)





~~~

Cargar bastante pdf para hacer un modelo mas grande de embeddings a ver que pasa


~~~


~~~


## Modelos Probabilisticos (Modelos de Markov)

Aplicabilidad Universal de los modelos de Markov

Finanzas.
Aprendizaje por refuerzo.
Modelos Ocultos de Markov.
Cadena de Markov Monte Carlo (MCMC).

Propiedad Fundamental de los Modelos de Markov.

Es como cunado solo consideras el clima de hoy para predecir el de mañana, ignorando como estuvo la semana pasada.

Estructura y Entrenamiento de un Modelo de Markov

Definicion y Componentes del modelo . Si esta Soleado, Lluvia, Nublado, etc.
Matriz de Transicion de Estados.
Entrenamiento del Modelo.

Aplicaciones en el PLN (Proceso de Lenguaje Natural).

Clasificacion de Texto(spam).
Generacion de Texto Original(Poemas).
Diferencia entre Aprendizaje Supervisado y no supervisado.

Resumen:

Los Modelos de Markov son esencialmente sistemas que pasan de un estado a otro con ciertas probabilidades.

Estas probabilidades no dependen de como llego al estado actual, sino solo del estado actual en si.

## Modelos de Markov

Representacion Matematica:

Si tenemos tres estados: A,B,C. La probabilidad de pasar de A a B prodria ser representada por P(B|A)

A representa que esta soleado y B que esta nublado, P(B|A) es la probabilidad de que se vuelva nublado dado que hoy esta soleado.

Uso de los modelos de Markov para Secuencias:

Puedes usar un Modelo de Markov para predecir la siguiente palabra basandote en la actual.

Ejemplo: Supon que despues de la palabra cierlo, la palabra azul aparece un 80% de las veces. Entonces:
     P("azul"|"cielo")=0.8

Estados en Modelos de Markov

Definicion de Estados y simbolos Categoricos:
    Ejemplo: En un modelo de Markov para prever el clima, los estaedos podrian ser "Soleado","Lluvioso" y "Nublado".
    Los estaos los declararemos como S(de State)

Notacion y Representacion:
    Usando la notacion anterior, "si" puede ser "Soleado" y "sj", "Lluvioso". La probabilidad de que despues de un dia soleado venga uno dia lluvioso es 
    P(sj|si).

Convencion de Numeracion de los estados:
      Soleado=1,Lluvioso=2,Nublado=3.

Distribucion de Probabilidad de los estados:
     La suma de las probabilidades de transicion desde "Soleado" a todos los otros estados (incluyendo quedarse en "Soleado") es 1.


Transicion de Estados y Matrices de Transicion.

Dependencia de los estados Anteriores:
    Despues de un dia "Soleado", la probabilidad de que el siguiente sea "Lluvioso" no depende de si los dias anteriores fueron soleados o lluviosos.

Distribuciones Condicionales y Valores de Probabilidad:
     P("Lluvioso"|"Soleado")=0.4 y P("Nublado"|"Soleado")=0.6

Matriz de Transicion de Estado (Matriz A)

Homogeneidad en el Tiempo en Modelos de Markov

Distribucion del Estado inicial (Pj)
     Al inicio de una secuencia, no hay un estado anterior del que depender. Por eso, necesitamos una distribucion de probabilidad inicial para determinar el primer estado.
     Pi=[0.6(soleado),0.3(Nublado),0.1(Lluvioso)]

<img src="./img/Markov_matriz_transicion.PNG" />

Representacion en Python

transiciones = {
   'A':{'A':0.6,'B':0.3,'C':0.1}
   'B':{'A':0.2,'B':0.7,'C':0.1}
   'C':{'A':0.2,'B':0.3,'C':0.5}
}

Implementacion Computacional y Entrenamiento.

Podemos usar bibliotecas de Python como NumPy para ayudar a representar y manipular matrices y vectores.

Con la matriz de transicion y Pi, podemos calcular la probabilidad de una secuencia especifica usando un simple bucle.

Usando datos historicos, podemos "entrenar" nuestro modelo ajustando las probabilibades hasta que representen mejor nuestros datos.(obtener matriz de transicion a partir de historicos).

Si observamos que despues de 100 dias soleados, 70 resultaron ser nublados al dia siguiente, la probabilidad de transicion seria 0.7.

## Suavizado y probabilidades logaritmicas

### Estimaciones de Maxima Verosimilitud.

P(word2|Word1) = count(word1,word2)/count(word1)

Si la palabra "perro" aparece 100 veces en el dataset y la secuencia "Perro ladra" aparece 10 veces entonces P(ladra|perro)=10/100=0.1

### Problema de Valores Cero:

P(word2|word1)=count(word1,word2)/count(word1)

Si intentamos calcular la probabilidad de una secuencia y alguno de los valores resulta ser cero(porque ciertos pares de palabras no aparecieron en el conjunto de entrenamiento), toda la expresion se vuelve cero.

Ejemplo: Si la secuencia "gato vuela" nunca aparece, entonces P(vuela|gato)=0

Esto no es deseable, ya que una frase no deberia ser considerada imposible solo porque contiene un par de palabras que no se encontraron en el conjunto de entrenamiento.

### Solucion: Suavizado

P(word2|word1) = count(word1,word2)/count(word1)

Suavizado +1
    Ejemplo: Si nuestro dataset hay 1000 palabras unicas y la secuencia "gato vuela" nunca aparece, entonces:
       P+1(vuela|gato) = 0+1/count(gato) + 1000

Suavizado Epsilon
    Ejemplo: Usando epsilon=0.1 y suponiendo 1000 palabras unicas, para "gato vuela"

          P Epsilon(vuela|gato) = 0+1/count(gato + 100*0.1

### Probabilidad de una secuencia

P(secuence) = P(word1)*P(word2|word1)*...*P(wordn|wordn-1)

Donde:

P(word1) es la probabilidad de que aparezca la primera palabra.
P(word2|word1) es la probabilidad de que la segunda palabra apareceza despues de la primera:
P(wordn|wordn-1) es la probabilidad de que la ultima palabra aparezca despues de la penultima palabra.

Ejemplo:

Vamos a utilizar la secuencia "el gato duerme":

La probabilidad de que la palbra "el" aparezca al inicio es P(el).
La probaiblidad de que la palabra "gato" siga a "el" es P(gato|el).
La probaiblidad de que la palabra "duerme" siga a "gato" es P(duerme|gato).

Si cada una de estas probabilidades es 0.01(es decir, 1% de probabilidad):

P(sequence) = P(el)*P(gato|el)*P(duerme|gato)

P(sequence)= 0.01*0.01*0.01
P(sequence)= 0.000001

Esto significa que, basado en nuestro modelo historico hipotetico, la probablidad de que la frase "el gato duerme" aparezca en ese orden especifico es de 0.000001 o 0.0001%

### Probabilidad de una secuencia

Al intentar calcular la probabilidad conjunta de una secuencia(especialmente en lenguaje), se termina multiplicando muchos numeros pequeños, lo que puede llevar a errores numericos o "desbordamiento por debajo" (underflow).

Esta problematica ocurre porque la multiplicacion de valores pequeños resulta en numeros aun mas pequeños. Una computadora podria redondear estos valores extremadamente pequeños a cero, lo que genera errores en los calculos.

### Solucion: Espacio Logaritmico

En lugar de trabajar directamente con probabilidades, se propone trabajar con logaritmos de probablidades

La ventaja es que la suma de logaritmos es mas numericamente estable que la multiplicacion de probabilidades. Ademas , sumar es computacionalmente mas eficiente que multiplicar.

Es importante tener en cuenta que el logaritmo es una funcion monotonamente creciente, lo que significa que si un numero es mayor que otro, su logaritmo tambien es mayor. Asi, que trabajar en el espacio logaritmico no altera las relaciones de orden entre las probabilidades.

Formula:

log(P(secuencia)) = log(P(palabra1))+log(P(palabra2|palabra1))+...+log(P(palabran|palabran-1))

Ejemplo:

Para la secuencia "el gato duerme", si tomamos por simplicidad que cada palabra o par de palabras tiene una probabilidad de 0.01, en lugar de multiplicar estos valores:

P("el gato duerme")=0.01*0.01*0.01

En el espacio logaritmico, sumariamos los logaritmos de estas probablidades:

log(P("el gato duerme")) = log(0.01)+log(0.01)+log(0.01)

Si utilizamos logaritmos en base 10, entonces log(0.01)= -2 por lo que:
log(P("el gato duerme"))=-2*-2*-2=-6

## Modelos de Markov y clasificacion de Texto. Construccion de un generador de Texto.

### Introduccion

Aplicacion de modelos de markov para construir un clasificador de texto

Trasladar la teoria a una aplicacion real.

¿Que es un clasificador de Texto?

Modelo que toma una texto como entrada

Predice su categoria

Ejemplo: Diferenciar poemas

### Aplicaciones del clasificador de Texto

Predecir si un correo es spam

Determinar si una critica de pelicula es positiva o negativa. Analisis de sentimiento.

### Objetivo del Ejemplo

No es construir el clasificador mas preciso.

Practicar y entender lo aprendido.

### Modelos de Markov y Clasificacion de Texto

Clasificacion de texto es aprendizaje supervisado.

Modelos de markov son no supervisados.

Usamos la Regla de bayes para combinar ambos.


Modelos de Markov y Clasificacion de Texto.

Clasificacion de texto es aprendizaje supervisado.

Modelos de Markov son no supervisados.

Usamos la Regla de Bayes para combinar ambos.

### Regla de Bayes y Clasificacion

P(spam|Premio)=P(Premio|Spam)*P(Spam)/P(Premio)

## Construyendo un clasificador con Python


~~~
import numpy as np
import matplotlib.pyplot as plt
import string
from sklearn.model_selection import train_test_split

archivos =['Benedetti.txt','Neruda.txt']

textos=[]

etiquetas=[]

#etiqueta es el indice
for etiqueta,f in enumerate(archivos);
    print(f"{f} corresponde a {etiqueta}")

    with open(f,'r',encoding='utf-8') as archivo
         for line in archivo:
            print(line)
            line=line.rstrip().lower()
            if line:
               # eliminar signos de puntuacion
               line=line.traslate(str.maketrans('','',string.punctuation))
               textos.append(line)
               etiquetas.append(etiqueta)

train_text,test_text,Ytrain,Ytest = train_test_split(textos,etiquetas,test_size=0.1,random_state=42)

indice =1
indicepalabras={'<unk>': 0}

#Construccion de un Diccionario de Codificacion de Palabras o Indices

for texto in train_text:
    tokens=texto.split()
    for token in tokens:
        if token not in indicepalabras:
           indicepalabras[token]=indice
           indice +=1

# convertir datos a anteros
train_text_int=[]
test_Text_int=[]
for texto in train_text:
     tokens = texto.split()
     linea_entero = [indicepalagras[token] for token in tokens]
     train_text_int.append(linea_entero)

train_text_int

# get(token,0) significa que me traes el indice del token y si no esta por el indice 0
for texto in test_text:
    tokens=texto.split()
    linea_as_int=[indicepalabras.get(token,0) for token in tokens]
    test_text_int.append(linea_as_int)

V= len(indicepalabras)
# solucion del suavizado
A0=np.ones((V,V))
pi0=np.ones(V)

A1 =np.ones((V,V))
pi1= np.ones(V)

def compute_counts(text_as_int,A,pi):
     for tokens in text_as_int:
         last_idx=None
         for idx in tokens:
         # estamos en la primera palabra de la secuencia
         if last_idx is None:
             pi[idx] += 1
         else:
             A[last_idx,idx] +=1
         last_idx = idx

compute_counts([t for t, y in zip(train_text_int,Ytrain) if y==0],A0,pi0)
compute_counts([t for t, y in zip(train_text_int,Ytrain) if y==1],A1,pi1)

# Normaliza A y pi para que sean matrices de probabilidad validas 
# Convencete de que esto es equivalente a las formulas mostradas anteriormente

A0 /= A0.sum(axis=1,keepdims=True)
pi /= pi0.sum()

A1 /= A1.sum(axis=1, keepdims=True)
pi1=pi1.sum()

logA0=np.log(A0)
logpi0 = np.log(pi0)

logA1 = np.log(A1)
logpi1= np.log(pi1)

count0 = sum(y==0 for y in Ytrain) # Cuenta de etiquetas de clase 0 en Ytrain
count1 = sum(y==1 for y in Ytrain) # Cuenta de etiquetas de clase 1 en Ytrain

total=len(Ytrain)  # Cantidad total de ejemplos entrenamiento
p0 = count0/total  # Probabilidad a priori de clase 0
p1 = count1/total  # probabilidad a priori de clase 1
logp0 = np.log(p0) # Logaritmo de la probabilidad a priori de clase 0
logp1 = np.log(p1) # logatitmo de la probabilidad a priori de clase 1

p0,p1  # imprime las probabilidades a priori de ambas clases

# Construccion de un clasificador

class Classifier:
     def __init__(self,logAs,logpis,logpriors):
           self.logAs=logAs
           self.logpis=logpis
           self.logpriors = logpriors
           self.k = len(logpriors) # numero de clases

     def _compute_log_likelihood(self, input_,class_):
         logA = self.logAs[class_]
         logpi = self.logpis[class_]

         last_idx= None
         logprob =0
         for idx in input_:
             if last_idx is None:
                 # Es el primer token en la secuencia
                 logprob += logpi[idx]
             else:
                 # Calcula la probabilidad de transicion de la palabra anterior a la actual
                 logprob += logA[last_idx,idx]
             # Actualiza last_idex para la proxima iteracion
             last_idx = idx
         return logprob
     
     def predict(self,inputs):
          predictions = np.zeros(len(inputs))
          for i,input_ in enumerate(inputs):
               # Calcula los logaritmos de la probabilidades posteriores para cada clase
               posteriors = [self._compute_log_likelihood(input_c,c) + self.logpriors[c] \
                               for c in range(self.K)]
               # Elige la clase con la mayor probabilidad posterior como la prediccion
               pred = np.argmax(posteriors)
               predictions[i] = pred
          returns predictions

clf = Classifier([logA,logA1],[logpi0,logpi1],[logp0,logp1])

Ptrain = clf.predict(train_texgt_int)

print(f"Train acc:{np.mean(Ptrain==Ytrain)}")

Ptest = clf.predict(test_text_int)
print(f"Test acc:{np.mean(PTest == YTest)}")



~~~

## Generacion de texto con Modelos de Markov

### Introduccion

Usar modelos de markov para generar textos.
Aprendizaje no supervisado (no necesitamos etiquetas)

## Ampliacion de modelos de Markov

Problema de modelos de markov

La -> Casa -> del -> perro -> ??

## Modelo de Markov de segundo orden

Nueva manera de almacenar y representar las probabilidades de transicion:

La matriz tridimensional a se representa de la siguiente manera:
    
    aijk = P(Xt=k|Xt-1=j,Xt-2=i)

Donde:
Xt representa el estado en el tiempo t.
aijk es la probabilidad de que, dado que el sistema estaba en el estado i en el tiempo t-2 y en el estado j en el tiempo t-1, estara en el estado k en el tiempo t.


### Implicancias

Una preocupacion es que a medida que aumenta le numero de estados anteriores que consideramos, el tamaño de la matriz "a" (o tensor) crece exponencialmente.
Este crecimiento podria llevar a problemas de eficiencia computacional y requerir recursos significativos para su implementacion y calculos.







---

## Procesamiento del Lenguaje Natural, uso de bibliotecas como NTLTK y SpaCy - "Data & Analytics"

https://www.youtube.com/watch?v=0tmWnPXiCos

NLTK
spaCy
---
## Aprende a analizar texto con Python y NLTK + Despliegue en GitHub

https://www.youtube.com/watch?v=YlVbwHGDoMU

nltk



---

## Laboratorio práctico con spacy y python para el procesamiento de textos

https://www.youtube.com/watch?v=l7v4poqH-JY

spacy

---

## Uso de la librería Spacy de Python para procesamiento de texto

https://www.youtube.com/watch?v=BfxWSEvWNQM

spacy


---
## Spacy Procesamiento de Lenguaje Natural (NLP)

https://www.youtube.com/watch?v=dK97CUQ8T1E

spacy


---
## Procesamiento de Lenguaje Natural - Generación de Texto

https://www.youtube.com/watch?v=uZ2bH5O_8f0

RNN

Arquitectura CharRNN

pytorch

---
## TextBlob + WordCloud: Análisis de sentimientos y nube de términos

https://www.youtube.com/watch?v=kOJtAwootsw

basada en nltk


---

## Generating Poetic Texts with Recurrent Neural Networks in Python

https://www.youtube.com/watch?v=QM5XDc4NQJo

---




---