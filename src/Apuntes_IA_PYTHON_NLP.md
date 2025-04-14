# Apuntes procesamiento de lenguaje natural

---
## Curso Completo de Procesamiento de Lenguaje Natural (NLP) con Python

https://www.youtube.com/watch?v=9x1QtYNLJRY

Codigo espinoza


-bolsa de palabras

-El orden de las palabras

-metodo de conteo
las ocurrencias o frecuencia con que aparecen cada palabra en el texto o secuencia de palabras.

-Tokenizacion
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

-Stop words o palabras de parada

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


-STEMMING Y LEMMATIZATION

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

- Similitud de vectores

Similitud de documentos.
Spinning de articulos y SEO. (spining) variar el articulo, y que diga lo mismo con otras palabras
Recomendaciones.
Chat bots.

- Calcular Similitud de Vectores

Distancia Euclidiana

Angulo entre vectores. Distancia coseno

En el procesamiento del Lenguaje Natural, a menudo se prefiere la similitud del coseno porque toma en cuenta el angulo entre los vectores, que pueden ser mas relevante en contextos donde los vectores representan textos o palabras.

- Metodo TF-IDF

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

-Aplicacion TF-IDF. Recomendacion de peliculas


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


- Neural word embedings

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


- Ejemplo de Word Embeddings : Analogias

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


-Crear tus propios Embeddings con word2vec

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