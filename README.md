# Google Cloud for Big Data and Machine Learning

Con la nube puedes estar operando todo el año sin reiniciones por mantenimiento. 
Además tienes algo que va a estar funcionando sin fallos. Si se cae esto, es que se ha caído Google. 

Hay niveles de nuevo;
- Google compute engine.
- Deplayment manager.
- Managed VMs.
- App Engine (servidor de aplicaciones).

La elasticididad que te da la nube es enorme. Pero ojo, no es gratis. Hay que saber lo que necesitas y no matar moscas a cañonazos (usar más capacidad de nube de la necesaria).

Los data centers de Google han tenido que pegarse con nucho tráfico (Youtube tiene el 40% del trafico de internet), por lo que tienen mucha experiencia. Tienen un SO virtualizado basado en linux que tratan todo el contenedor como una máquina virtual. Tienen racks completo con CPU, memoria, almacenamiento, etc conectado con una red de alta velocidad (petabit). Cualquier máquina que compremos de Google tendrá parte de cada uno de ellos. Nostoros la vemos como una máquina virtual, pero por debajo está distribuidio => Si algo falla, nos dan otro son que nos enteremos. 

Tienen además una latencia muy baja que para Big Data a lo mejor no es relevante, execepto para streaming. Pero para web si es importante. 

Eficiencia en cuanto a operaciones. Neceistan mucha menos gente para operar estos data centers que para los tradicionales. 

Eficiencia energética y renovables: los data centers de Google son capaces de operar hasta casi 30 grados sin problemas a diferencia de los otros que son a 20. En Finlandia lo refrigeran con agua de mar directamente. 

Contenedor => Mayor granularidad que las MV. => Mayor estabilidad. 


Spanner: base de datos relacional pero que tiene la ventaja de las relacionadles: tiene escalabilidad horizontal (que en principio no era posible con relacionales por la necesidad de mantener integridad referencial de los datos). Esta seran el futuro. PAra los nuevos casos él la montaría así directamente. PEro el coste de mover algo existene ahí es mayor. 

Sobre networking, lo más inteteresante es la interconexión. Si quiero pasar datos desde mi máquina a google, puedo usar una VPN para conectarme directamente de forma encriptada. Los datos irán más seguros. 

DiagloFlow: es un servicio de atención al cliente. Mantiene una conversación aparentemente natural con preguntas que acaba generando una salida. Por ejemplo, te pregunta que quieres comer, si quieres ir en coche, etc. y al final te genera la reserva automáticamente . 

Codelabs: para hacer ejerciios y aprender. Vamos a hacer en clase los siguientes:
- Creating a Virtual Machine. 
- Upload Objects to Cloud Storage. 

# Big Data

En un minuto en google tienen 3M de busquedas , 100 horas de video y 1000 androids nuevos cada minuto... Volúmenes de datos terribles. 


# Pub/Sub

Equivalente a Apache Kafka. Para colas de mensajes. Permite pasar mensajes entre los distintos servicios de Google o propios. El reatin dura 7 dias maximo. Kafka lo puede hacer de forma indefinida. Kafka lo hace en menos de 5ms. PubSub tiene una latencia de en torno a un segundo. Uso frecuente: Google para las notificaciones de gmail. Para Big Data: informacion en tiempo real desde distintos sectores, por ejemplo de los aerogeneradores. Cualquier cosa que genere datos en tiempo real. 

Dos tipos de subscripciones:
* Push llega sin una subscripcion previa. 
* Pull llega si nos hemos subscrito. 

Puede almacenar cuando haya una caida (último estado). Tambien permite prevenir sobrecarga de mensajes. Hay clientes que tienen teras por segundo y no hay problemas!

# DataProc

Para ello, antes tenemos que conoce3r sobre distintos conectos. 

Dentro de un cluster Haddop/Spark, nos vamos a encontrar tres tecnologias clave:
* **HDFS**: Sistema de alamcenamiento de ficheros distribuido. Tengo una serie de discos en mi cluster. Cada fichero está distribuido en los distintos nodos (replicado). Cuando haga algún tipo de procedo que requiere leer el fichero grande, usaré varios workers que vayan leyendo en paralelo el documento de los distitnos discos en los que está replicado. Por ejemplo, si lo tengo en tres sitios, le digo que lea un tercio con cada uno. Además, si perdiera un disco, sigo pudiendo hacer cosas. Asi es como almacena los datos el sistema BigQuery de Google. 

* **Hadoop**: La primera era de Big Data. Permite hacer el algoritmo de map/reduce. Es computacion paralela, Divide entre varios nodos, N, el trabajo el trabajo y tarda N veces menos aproximadamente. Hay un nodo master que distribuye el juego y N esclavos que hacen el trabajo. Si uno de esos N tiene problemas (disco, memoria, etc.). El master se da cuenta y genera otro exactamente igual que haga su trabajo. Eso es el patron YARN (Yet Another Resource Negotiator). Es en java. Para hacer algo nuevo mejor no usarlo. 

* **Spark**: Es la siguiente generacion del big data. Con hadoop nos encontramos la limitacion de lectura y escritura de los discos. Spark te permite el mismo patrón YARN pero en memoria. Es lo mismo, pero el otro va en disco y este en memoria. 

Hay cosas por encima: SparkSQL para abstraerte de lo de avbajo y hacer las cosas con SQL. PySpark lo mismo pero con python. 
Pig y Hive son abstracciones que van por encima de Hadoop y Spark tambien 

Dataproc nos permite usar tood esto sin tener que configurar nada, ya lo tiene todo instalado. Solo tengo que decir: quiero un cluster de 5 nodos y ya lo tengo sin configuración. 

* **Dataflow** : considera que es la tercer generacion. MEjor que  haddop y spark. 

DAtaflow serie interesatne tb para tmeas de procesar datos (scraping, etc(.
 CloudML Engine = Como data flow pero apra entrenar model

Ejemplos del mismo equipo de Google en Github

https://github.com/GoogleCloudPlatform/professional-services

**Apache Beam**: aprender de esto, que sabe poca gente y es la siguiente oleada. 

## Big Query

Es como si tuviera un cluster de spark con 1000 nodos => mucho más rápido. Además no me tengo que precoupar de gestionarlos. Una query de Teras de datos tardará del orden de segundos. Si es petabytes, será del orden de minutos. 

Sql Server tardaba 40 minutos y en Big Query son 2 minutos. Procesos de ETL de Bussiness Intelligence de 10 horas, con volumen de datos de 10 teras, se resuelven en 10 minutos. 

Además es más barato. Todo lo que podamos llevar a consultas SQL Estandar, el consejo es llevarlo a Big Query. Lo que tenga otras cosas, como llamadas a librerias, etc, montarlo sobre dataflow. 

Es computacion distribuitda tambien y riene un motor de consultas. 

Esto tiene determinadas herramientas en Big Query que no tiene el SQL Estandar. Por ejemplo, trasposicion de datos. 

Aquí la infraestructura es compartida. No es omo dataproc en el que tú te resevas tu máquina. Aquí los resucursos de capturan de forma 

Pero BigQuery no vale para hacer consultas para una web apra algo super rápido . PAra eso usar por ejempli Big Table. BigQuery tarda al menos un segundo.

En BigQuery tenemos un proyecto, despues un dataset y luego las tablas. Un dataset es una agrupación de tablas. Por ejemplo puedo tener un DataSet de RRHH y otro de financiero. Pues bien, BigQuery permite extraer datos de ambos dataset para las queries.

Además, permite otros datos de entrada, como de redes sociales, de SAP, de escripts de r, y multidud de formatos de salida, desde excel hasta un cutre-tableau. Y los datos de entrada pueden llegar también en streaming o en batch. 

Una de las razones por las que funciona bien es porque su almacenamiento está orientado a columnas en lugar de orientado a filas. Por ejemplo, si quiero saber todos las personas que se llamen Ismael, tiene que ir fila a fila. Sin embargo, con esto, habrá un _fichero_ para esa columna concreta, lo que acelera las búsquedas. 

Los datos también están particionados por día, aunque también se puede particionar por por ejemplo país. Todo esto es rendimiento aún más rápido. 

Con BigQuery, por cada tera de información , cobran 5 dólares .

## Datalab

Ya no tirar por datalab, que yq ni existe en la consola, sino tirar por la segunda opcion de las siguiente. 

Es para noetbooks de Jupyter. Aparte de éste, está :

* colab: ya lo vimos en su momento. Pero tiene limitaciones para uso empresarial. Ademas , puede que quieras hacer algo y no tengas recursos suficientes. De madrugada habrá más recursos. Pero no puedes personalizarlo. Además no es integrable con un git. Para probar nuestros modelos, sin problema. Cuando ya sea productivo, mejor cambiar a lo otro, que sabemos que va a estar disponible. 
* En la consola, ir a AI Platform>Notebooks: ahí ya tiene instancias con todo instalado. Ademas, puedo definir una máquina compaertida con mi equipo en la nube. Tambien puedo usar una imagen mas barata para mis pruebas y despuues coger una mas potente para el entrenamiento. Una potente puede tener 1 terabytes de ram y 50 procesadores, por ejemplo. Con eso si puedes gestionar esos notebooks en un git.  Puedo también añadir datos adicionales. Y puedo después guardar los datos en BigQuery. Puedo tambien usar CloudML para entrenar modelo y servirlo a traves de api. 

Interesante si vas a interactuar con Google. Tienes todo en el mismo sitio, te ahorras tiempos de bajada o subida de datos. 

REcomendacion: todo lo que sea cojsultas, mejor pedirsleo a bigquery en lugar de hacer consltas en pandas. Sera mas rapido y barato. 

## Cloud Composer/ Airflow

Ojo, el coste mínimo de entrada son de 300 euros al mes. 

Orquestador que me permite orquestar una ETL. Para hacer un workflow de datos. 

Pensado para procesos batch más que para streaming. 

Sencillo de codificar porque es con Python. 

Caso para un data scientis que esta explorando datos. Sube el csv u otor ficheor conocido a Big Query. Desde ahi, coge los notebooks de gmail para explorar, etc. (precio de guardar datos: 0.23 euros por giga y mes). Despues ya con el composer lo pondria en produccion. 

Tiene una componente visual muy buena parahacer insights dentro del propceso.

## Data Fusion

Está en beta de momento. 

También es para crear pipelines con datos. 

Si montas una instancia enterpreise son 1000 euros al mes. PAra aprender, tenemos una instancia de desarrollo con menor infraestructura por 100 euros al mes. 

Composer puede orquetar todos los servicios de google y de terceros, includios data fusion. Fusion integra datos, pero no puede orquestar como lo hace composer. 

El publico objetivo de Composer es un data engineer que sepa de python, el de Fusion, una data analiys que quieres hacer cosas rapidas sin necesidad de programar. Mas barato el composer. 
