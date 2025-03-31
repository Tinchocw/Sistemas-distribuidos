# EJ 5 


## Grupos 

* Poder permitir que los procesos armen colecciones entre ellos, que puedan mandar mensajes en este grupo y  que apliquen algunas entidaddes del grupo.
* Siempre el objejetivo es la comunicación.
* Los procesos se deben poder suscribir a un grupo, y desuscribirse. Deben haber primitivas para que esto suceda.
* Difusión de mensajes: revibir y entregar hacia alguien más cierto elemento. Puede tener distrintos casos:
    * Uni-cast: un proceso envía un mensaje a otro proceso.
    * Multi-cast: un proceso envía un mensaje a un grupo de procesos.
    * Broad-cast: un proceso envía un mensaje a todos los procesos.
    * Anycast: un proceso envía un mensaje a uno de los procesos de un grupo(no necesariamente a todos).


En el caso de anycast y unicast puedo tener un protocolo que sería el envio al nodo más cercano. (ECMP).


### Ej 

* Colecciones de grupos dinamicas, puede haber un grupo de 10 procesos, y que se vayan agregando y sacando procesos.



## Topologóia 

Puedo hacer el mismo envio de mensajes en distintas topologías. Pero la implementación en la misma va a ser distinta. 

* Topología de anillo: el mensaje va a ir de nodo en nodo hasta llegar al destino.
* Topología de árbol: el mensaje va a ir de nodo en nodo hasta llegar al destino.
* Topología uno a uno: el mensaje va a ir de nodo en nodo hasta llegar al destino. ???


Disfusción de los mensajes: Ver quien es el que coordina el envio de los mensajes. En el caso de que estemos en la **topología del arbol** peuden pasar dos situaciones:

* El nodo raiz es el que coordina el envio de los mensajes. Control centralizado en el nodo padre, habla con cada uno de los nodos hijos
* En este caso la responsabilidad de seguir comunicado con los nodos hijos es de los nodos hijos. Control descentralizado, cada nodo se encarga de hablar con sus hijos. **Este es el caso más correcto*

La decisión tomando en cuenta la topología es importante, ya que si tengo una topología de anillo, no puedo tener un control centralizado, ya que no tengo un nodo padre.


## Atomicidad de los mensajes

* Los mensajes deben enviarse a todos los procesos o a ninguno. No puede haber un caso intermedio.
* Necesidad de realizar ACK de los mensajes. Esto tiene que ver con la capa de aplicación que justamtente lo que buscamos es confirmar a los demás que recibií, comprendí y estoy listo para seguir adelante.
* Necesidad de demorar el delivery de los mensajes. 
* Reintentos frente a: 
    * Caida de receptores 
    * Caida de coordinadores 


## Midleware 

* Sofware de conectividad que ofrece un conjunto de servicios que hacen prosible el funcionamiento de aplicaciones distribuidas sobre plataformas homogeneas. Tiene que ser distinto sofware, IOT, sistemas envevidos.

BUSCAR IMAGEN DE MIDLEWARE




### Objetivo 



* Transparencia (vista unificada del sistema)
    + No es necesario saber que el sistema esta distribuido. Para mi accedo a cierto recurso y es trnasparente para mi si esta distribuido o no.
    *  Transparencia respecto a la capa de acceso, ubicación, migración y relicación, concurrencia fallos y persistencia. 

* Tolerancia a fallos
    * Sistemas confiable(no es que no falla nunca, pero puede tener la posibilidad de recuperarse) que se ejecuten y comporten de manera predecible incluso en presencia de fallos.


* Acceso a recursos compartidos
* Interfaces. Como soy independiente de las maquinas tengo que saber como comuncarse con todas las capas.
* Comunicación de  grupos. 
    * Permiten un broadcasting y multicasting de mensajes.
    * Facilitar localización de elemnentos y coorinación de tareas.


## Vista Fisica 

### Centralizado

Tenemos una unica maquina a la cual nos tenemos que comunicar con ella.

* Tiene un solo punto de falla
* Miniza la cantidad de mensajes a la red
* Si hay un problema esta en un solo lugar posible.
* No puede escalar. En la imgan son las instancias de computo que tiene mi monolito. LO VAN A HABLAR EN OTRA CLASE.

### Distribuido

Servicio que se provee en un espacio fisico. 

* Si falla una operación, en un principio no sabes donde esta el problema.
* Puede escalar. Tiene que estar bien balanceado para que pueda escalar.



## Clasificación 

### Transacciones de procesos

*  Permiten garantizar transaccionabilidad de operaciones respecto de datos.
* Conectar muchas fuentes de datos y permite un acceso transparente al grupo.
* Poseen politicas de reinitentos y retención de datps frente a caidas internas.


### Orientado a objetos

* Mensajes hacia sistemas distribuidos.
* Los objetos viven dentro del mideleware.


Tenemos el caso de un juego de shooting en el que el midleware va a ser el que tenga todos los obetos y va a decidr quien es el que vive y el que muere. VER BIEN



### Orientados a procesos

* El midleware trabaja como un servidor de fincipones que se pueden invocar remotamente.
* Los servicios se pueden explirar y ejecutar pero no presentan estado para futuras invocaciones.


### Orientado a mensajes MoM(es el que vamos a estar usando)

* Funcionan como un sistema de messajeria entre las aplcaciones que usen el midleware.
* Pueden enviarse mensajes bajo cierto "tópico" para que aquellos intereados los reciban(inforamtion Bus). INVESTINGAR
* Pueden enviarse mensajes con un destinatario definido (modo queue).




# Web Crawler 

Un web crawler es un programa que navega automáticamente por Internet para recopilar información de páginas web. Es la base de motores de búsqueda como Google, pero también se usa en muchas otras aplicaciones, como análisis de datos y monitoreo de cambios en sitios web.



* Es un programa que se encarga de navegar por la web y recolectar información.

* Como arranca el sistema - alguien entra a la pagina(URL) y le dice que empiece a navegar. 
* Arranca el fetch de la URL.


Quiero hacer pasos más grandes e ir rapido.


Pasos: Aplicación cliente donde esta el web crawler. Este le pasa a un sistema el pedido -- esto va a entrar en una queue -- y va a haber un sistema que va a estar procesando estos pedidos para poder hacer alguna de las tareas(por ejemplo el fetch), este va a ser el fetch controller.

Diagrama de robustez:
* Control(Controler) -- ejecutar == CPU == algo vivo haciendo computo -- procesamiento de información 
* Entity -- algo que tiene estado y que se puede guardar en una base de datos
* Boundary -- algo que se comunica con el exterior. Capa limite de cierto sistema, con la cual se comunica con el exterior.









