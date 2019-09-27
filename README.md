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

