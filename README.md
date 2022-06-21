#TRABAJO FINAL BIG DATA UPA 2022
Presentado por Matthew Fehr

Componente 1:Data Fetching
Este componente del código tiene cómo el objetivo de extraer datos
relacionados a un # a elección. En este caso está configurado para traer los 300
tweets más recientes que contienen el "#Tesla".

Pero antes de nada hay que preparar el API que va darnos acceso a la red social para sacar estos datos.
Para eso usamos las credenciales que están guardados en el documento twitter_api_log.csv. 
En el caso de correr el código en un ambiente local, solo hay que tener los archivos .csv que vamos a utilizar, 
en la misma carpeta que está guardado el código fuente. En el caso de que se corre el código en un ambiente externo
como el Google Colab, entonces se va requerir descomentar las partes del código que dicen "Upload to Drive".
De ahí se tiene que buscar entonces manualmente el archivo indicado.

Después de tener nuestro API de Twitter listo y extraemos los tweets, hay que sacar los componentes deseados.
En este caso solo queremos guardar las siguientes columnas de datos:
tweet 		= El contenido de texto del tweet en si
name_author 	= El nombre del autor que escribió el tweet
user_tag 	= El @ del usuario lo cuál es único en la red y con la cúal uno le puede buscar
favourite_count = La cantidad de "me gusta" que fueron dados al tweet
retweet_count 	= La cantidad de veces que el tweet fue republicado por otros usuarios en la red
created_at	= El timestamp del momento en el cuál fue publicado el tweet

Esto datos entonces al final guardamos en un documento CSV llamado en este caso "tweets_crudos.csv"


Componente 2: Data Analysis
Este componente del código tiene cómo el objetivo de analizar los tweets que fueron extraídos en el componente anterior.
En este caso usaremos el análisis de VADER ya que es muy buena para analisis de redes sociales porque tiene en cuenta
varios componentes cómo los emoticons, las palabras mayúsculas, la puntuación y mucho mas.

Primeramente vamos a importar el CSV del último componente en un nuevo dataframe. Otra vez se debe tener en cuenta si se 
está ejecutando de manera local o en la nube y seguir los mismos pasos de subida como en el componente anterior. 
Aunque esta forma de analisis maneja bien con textos de las redes sociales, vamos a realizar una limpieza básica de los tweets
para facilitar un poco el análisis. Después de eso lo tokenizamos y sacamos los stopwords. Al final nos quedamos entonces con el tweet 
con limpieza básica y una columna de "Lemma". A esta columna de lemma le aplicamos entonces la función de análisis de VADER y guardamos 
los resultados en una columna "Vader Sentiment". Estas puntuaciones entonces podemos categorizar con otra función en tres categorias;
positivo, negativo y neutral. Estas categorizaciones son guardados en otra columna llamado "Vader Analysis".
Para tener mas entendible los resultados del análisis Vader, podemos graficarlo en una torta de matplot.

Y al final podemos exportar los resultados del análisis en un documento CSV llamado en este caso "tweets_analizados.csv" en donde las columnas son:
tweet		= El texto de los tweets ya con una limpieza básica
Lemma		= La forma lemmatizada de los tweets
Vader Sentiment	= Una puntuación del contenido de Lemma con el sistema de análisis VADER, lo cuál tiene un rango de -1 a 1
Vader Analysis	= Una categorización de los resultados del Vader Sentiment, dividido en positivo, negativo y neutral