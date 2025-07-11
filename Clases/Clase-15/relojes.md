# Tiempos

## Relojes físicos

Cada computadora tiene su reloj local(este no esta sincronizado con el de las demás computadoras, a menos que una referencia lo sincronice), pero además hay un reloj universal que es el mismo para todas las computadoras. Este reloj universal se llama UTC (Tiempo Universal Coordinado) y es el tiempo estándar que se utiliza en todo el mundo.

El reloj global a ser un aparato conectado a internet que va a estar sincronizado con el reloj universal. Este reloj global va a ser el que se va a utilizar para sincronizar todos los relojes locales de las computadoras.

<div style="text-align: center;">
   <img src="image.png" alt="alt text" width=700">
</div>

Drift: Error del reloj, descalibre del reloj por distintas situaciones de temperatura, humedad, etc. Por lo que los relojes no son confiables para su comparación.

## Referencias globales

- UTC (Tiempo Universal Coordinado) --> Basado en medición por relojes atómicos, este recibe ajutes atomicos)
- GPS Time (Tiempo GPS)
- TAI (Tiempo Atómico Internacional) -- no recibe ajustes astronomicos.

### Drift

**Drift:** Cambios de temperatura, presión y humedad descalibran relojes.

- Los relojes físicos no son confiables para su comparación por efecto del dirft.

- Hay que sincronizar periodicamente:

  - Medir el desvío medinte el valor de referencia(UTC o GPS).
  - Aplicar la correción o compensación lineal cambiando la frecuencia del reloj local.
  - Nunca atrazar el reloj, hay que avanzar el reloj más lento.

- Hay que sincronizar al despertar la computadora.

<div style="text-align:;">
   <img src="image-9.png" alt="alt text" width=500">
</div>

### Algoritmo de Cristian

Realiza una compensación del delay existente al obtener la medida de tiempo. Este algoritmo esta tomando en cuenta el delay de la red para la comunicación entre el cliente y el servidor para poder obtener el tiempo correcto.

- T0: El client envia request
- T1: El cliente recibe respuesta.
- Hipotesis: Delays en la red son constantes.

Entonces el nuevo tiempo de la computadora que se sincrnizo es igual al tiempo del servidor en el momento que recibió la solicitud más la mitad del tiempo que tardó en recibir la respuesta, que sería el tiempo que tardo en volver el mensaje.

<div style="text-align:;">
   <img src="image-1.png" alt="alt text" width=500">
</div>

## NTP (Network Time Protocol)

### Objetivos

- Sincronización:
  - Clientes(UTC) sincronizados aunque existan delays en la red.
  - Analisis estadistico para filtrar data y obtener resultados de calidad.
- Alta disponibilidad:

  - Sobrevivir a largas caídas de conectividad
  - Rutas redundantes
  - Servidores redundantes

- Escalabilidad:
  - Gran número de clientes sincronizados de forma frecuente
  - Debe tener en cuenta efectos de drift

### Estructura de NTP

<div style="text-align:;">
   <img src="image-3.png" alt="alt text" width=700">
</div>

- Estrato 0: Master clocks
- Estrato 1: Servidores conectados directamente a master clocks
- Estrato 2: Servidores sincronizados con servidores en estrato 1
- Estrato N: Servidores sincronizados con servidores en estrato N-1
- Servidores sincronizados entre sí con conexiones peer-to-peer. Esto se hace de esta manera ya que puede existir la posibilidad de que los servidores del estrato superior no respondan. Este servidor puede elegir repspoderlo o no, si lo hace es porque se condidera que el servidor es confiable.
- Mensajes enviados de forma no reliable (UDP puerto 123). Esto se hace para evitar el overhead de TCP. Como se transporta poca información y se envía de forma periódica, no es necesario que se garantice la entrega de los mensajes.

### Modos de sincronización

- Modo multicast/broadcast --> Baja precisión
  - Usado en LANs de alta velocidad
  - Eficiente pero de baja precisión --> No se puede hacer ninguna consideración del RTT.
- Modo Cliente-Servidor (RPC)
  - Grupos de aplicaciones se conectan formando un grupo
  - Aplicaciones entre sí no pueden sincronizarse
- Modo Simétrico (Peer Mode)
  - Peers sincronizados entre sí para proveer backup mutuo
  - Utilizado en estratos 1 y 2

## Relojes lógicos

**Evento**

- Suceso relativo al proceso Pi que modifica su estado

**Estado**

- Valores de todas las variables del proceso Pi en un momento dado
  Relación 'ocurre antes' (happened before):
- Relación de causalidad entre eventos o estados tales que:

  - a b, si a,b pertenecen al mismo proceso Pi y a ocurre antes de b
  - a b, si a es un evento de Pi, b es un evento de Pj, a es el envío del mensaje 'm' a Pj y b es la recepción del mensaje 'm' desde Pi
  - a c, si a b y b c (transitividad)

Si un evento paso antes que otro garantiza que el segundo evento no puede ser antes que el primero. Pero esto no funciona de la forma inversa.

Los procesos son los puntos, los números que ponemos arriba son lo que queremos medir.

Dado S, el conjunto de todos los estados locales posibles del sistema y "-->" la relación temporal de implicancia "happened before", un reloj lógico es una función C monotónica creciente que mapea estados con un número natural y garantiza que:

para todo evento s,t pertenciente a S, s es anterior a t si y solo si, los relojes lógicos cumplen la siguiente relación: C(s) < C(t)

<div style="text-align: center;">
   <img src="image-10.png" alt="alt text" width=600">
</div>

### Algoritmo de Lamport

Los valores de arriba son los valores de los relojes lógicos. Los números de abajo representan el estado de los procesos.

Cuando un proceso le envia un mensaje a otro, el proceso que envía incluye dentro del sistema su reloj lógico. El proceso que recibe, lo que va a hacer es tomar el valor del reloj lógico del mensaje y compararlo con su propio reloj lógico. Si el valor del reloj lógico del mensaje es mayor que el suyo, entonces va a actualizar su reloj lógico al valor del mensaje más uno.

Este algoritmo lo queremos usar para

<div style="text-align:;">
   <img src="image-11.png" alt="alt text" width=500">
</div>

### Inconvenientes

Lo que quiero hacer en este caso, es que si tengo el reloj lógico de s y de t poder determinar cual fue el evento que ocurrió primero, para saber si dos estado cualquiera son concurrentes o no concurrentes(siendo concurrentes aquellos estados que no cumplen con la condición "Happened before").Pero no puedo determinarlo con un único escalar. Esto se ve en el siguiente ejemplo:

<div style="text-align:;">
   <img src="image-4.png" alt="alt text" width=500">
</div>

El reloj de Lamport captura muy poca información sobre dos eventos:

1. progreso dentro de un proceso
2. progreso durante envíos de mensajes entre procesos
   pero se pierde la información de qué evento ha ocurrido se pierde al
   almacenar un único escalar.

<div style="text-align:;">
   <img src="image-12.png" alt="alt text" width=500">
</div>

No se puede determnar si el evento s1 ocurrio antes del evento t4 ya que no hubo un intercambio de mensajes entre los procesos. Esto sucede porque no tengo la información necesaria de ambos procesos para tomar esta decisión. Como se ve en las imagenes puede suceder cualquiera de las dos situaciones.

### Corolario

Cuando sucede esta situación estamos hablando de eventos **PARALELOS**

<div style="text-align:;">
   <img src="image-13.png" alt="alt text" width=500">
</div>

## Vectores de relojes

Un vector de relojes es el mapeo de todo estado del sistema compuesto por k
procesos, con un vector de k números Naturales y garantiza:

<div style="text-align:center;">
   <img src="image-14.png" alt="alt text" width=500">
</div>

donde s.v y t.v son los vectores de k componentes para los estados s y t
respectivamente y

<div style="text-align:center;">
   <img src="image-15.png" alt="alt text" width=500">
</div>

En pocas palabras, para determinar que un evento s ocurre antes que un evento t, tenemos que comparar los vectores de ambos eventos. Si el vector de s es menor al vector de t, entonces s ocurre antes que t.

Hay dos situaciones en la que esto no se puede determinar:

- Los vectores son iguales, entonces no se puede determinar si s ocurre antes que t o viceversa.
- Los vectores son paralelos, entonces no se puede determinar si s ocurre antes que t o viceversa. Esto es cuando los vectores son diferentes pero ninguno es mayor que el otro. En el caso de dos procesos, si un elemento del vector de s es mayor que el elemento del vector de t, pero otro elemento del vector de t es mayor que el elemento del vector de s, entonces no se puede determinar si s ocurre antes que t o viceversa.

<div style="text-align:center;">
   <img src="image-16.png" alt="alt text" width=500">
</div>

<div style="text-align:center;">
   <img src="image-17.png" alt="alt text" width=500">
</div>

# Sincronismmo

Depende del contexto:

- Sistemas distribuidos: Queremos medir los eventos en el tiempo
  - Steadiness: No queremos que los eventos se desincronicen
  - Tightness: Queremos que los eventos se sincronicen

Nos vas a interesar medir las propiedades para determinar que el sistema es estable.

- Tiempo delivery: Es el tiempo que tarda un mensaje en ser recibido luego de haber sido enviado.
- Timeout de delivery: Es el tiempo máximo que se espera para recibir un mensaje antes de considerar que ha fallado.

- Steadiness: Maxima diferencia entre el mínimo y el máximo tiempo de delivery de caulquier mensaje recibido por un proceso.

- Tighness:

## Protocolos Clock-driven

Los relojes necesariamente tienen que estar sincronizados

### Steady and Tight Protocol

Nos garantiza que el tiempo de delivery no va a ser mayor a un tiempo máximo. Pero no nos garantiza que el mensaje llegue. Por lo tanto no podemos garantizar que el mensaje llegue en un tiempo determinado.

### Steady and Tight TDMA Protocol

Medio compartido de comunicación. Si estamos todos hablando al mismo tiempo no nos entendemos, tenemos que ir tomando turnos.

Nos podemos asignar periodos de tiempo donde cada uno puede hablar.

Lo importante de estos protocolos es que hay una demora. Hay un envio del mensaje y un procesamiento del mesaje.

## Delivery de Mensajes | Hold-back queue

- Envio del mensaje no es lo msimo que procesarlo(delivery de los mensajes).

- El delivery consiste en procesar el mensaje provecando, eventualmente, cambio en el estado del proceso.
- Los mensajes se mantienen en una cola que permite controlar el momento en que se lo libera, permitiendo demorar el delivery.

## Orden sincronico

Todo mensaje posee el mismo timestamp que el mensaje que lo origina. La transmisión del mensaje es de tiempo nulo. (despreciable)

›![alt text](image-5.png)

## Orden FIFO

Para un emisor y un receptor, si el eminsor envia dos mensajes m1 y m2, y el receptor recibe primero m1 y luego m2, entonces el receptor no puede recibir m2 antes que m1.

![alt text](image-6.png)

## Orden causal

M1 envia mensaje a M3 e inicia otra comunicación.

nos interesa que si soy un receptor que recibo un mensaje y luego recibo otro sea consecuencia del otro, entonces quiero ver primero el mensaje que origina la comunicación y luego el mensaje que es consecuencia de esa comunicación.

![alt text](image-7.png)

En en caso del dibujo el caso anterior es si efectivamente le llego el mensaje d2 a P1.

## Orden total

Todo par de mensajes entregados a los mismos receptores es recibido en el mismo orden por esos receptores. Le importa que reciban primero el mismo mensaje.

No implica orden causal. Son dos cosas distintas.

# Estado

- Local: tengo un proceso y un momento, el estado es la unión de todas las variables de ese proceso.

- Global: La unión de los estados locales es el estado global.

Analogía:
Tengo un contador y cuando le hago click suma 1. Si miro para el otro lado y me cambian el contador. Que es lo que ese contador tendría que tener para que no me de cuenta que me lo cambiaron ?

Tendría que tener el mismo número que tenía en el contador.

En el caso de que se me rompa, para poder terminar la operación tengo que arrancar del último estado que tuve.

EJ 2:

Tengo una aplicación que es el contador, y me doy vuelta y me roban el celu. Saco otro, entonces voy a tener que tener el mismo estado de contador anterior y además neccesito la misma aplicación instalada en el nuevo celu.

La aplicación en este caso sería el código.

La entrada es el estado, pero también el código que estoy ejecutando(en este caso es la aplicación).

Ej 3

Tengo una computadora, el código lo damos por sentado porque esta en el disco. Si la aplicación me estaba mostrando una imagen, me la tendría que estar guardando una y otra vez ?

No me la tengo que estar guardando todo el tiempo, porque la imagen y el código son constantes, no son variables. Lo que esta cambiando en este caso el el número en si. Esta operación va a ser determinística.

Lo que pertenece al estado tiene que ser independiente de los demás elementos del sistema.

Ej 4

Emuldaores: Esta lo que se llama el safe state.

### Sistema con máquinas de estados

- Modelo de computación donde tengo un conjunto de variables.
- Ocurren eventos que me hacen pasar de un estado a otro.
- El estado en el que estoy se refleja en mis variables.
- Siempre arranco en un evento inicial y termino en otro evento final.

### Que pasa si tengo más procesos

Pasar de estado ocurre con el envio del mensaje.

![alt text](image-8.png)

### Historia y cortes de un sistema

No soy una maquina de estados. Sino que tengo un historial de lo que esta pasando.

- Historial
- Corte: Unión del subconjunto de historias de todos los procesos del sistema hasta

Si hago un corte que es consistente, tengo para cda procesos un historial de enventos. Si me me corta la luz lo que puede restaurar el estado sin tener que volver a empezar y comunicame nuevamente con el resto de los procesos.

Un ejemplo puede ser con el caso de una transacción. Si tomo el corte(saco la foto en donde es correcto) y lo guardo, puedo volver a ese estado. Si no tengo el corte, tengo que volver a empezar la transacción.

## Comunicación Reliable

- Que garantice la integridad de los datos.
- Validez
- Axtomicidad de los datos.

- Uno a Uno

  - Trivial si contamos con protocolos sobre TCP/IP y una red segura

- Uno a Muchos
  - El grupo debe proveer
