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

