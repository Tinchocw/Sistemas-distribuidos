# Clase 3 - Paralelización, Multiprocessors, Multicomputing

Copiar la primera diapo

* Camino critico: 

## Paralelización de tareas: Ley de Amdahl


Tengo tareas, una parte es paralelizable y la otra es serial(esto si o si va a estar).

La idea es que si yo tengo un solo procesador, lo que hago es hacer primero la parte serial y despues la parte paralelizable, en cambio, en el caso de tener más de un procesador lo que se hace es dejar la parte serial en un procesador y despues el paralelizable lo separo en los demas procesadores.

* Peor caso: Lo maximo que puedo tardar es si tengo un solo procesador.
* Mejor caso: Que pasa si tenog infinita paralelización, lo mejor que puedo lograr sería ... (ver en la clase).


Lo que nos dice amdahl es que todo trabajo que hagas que sea serial ...


## Ley de Gustafson 

El speedup no lo debes medirlo con una unica tarea sino que deberias medirlo escalando el problema.



## Modelo work-span

* Paralelismo imperfecto
* Greddy schedudling: Proceso 
* 


Estrategia de paralelización 


Descomposición funcional: Tengo una fución con tres dentro funciones dentro de la misma. Lo que hago es poder paralelizar la funciones que tengo dentro de la misma 


Particionamiento de datos: Los datos se deben poder separar, la función se pueda separar. La idea es separar los datos para poder paralelizar, se va a hacer un fork y un join en algun momento.



 ## Patrones de procesamiento

* Basados en algoritmos
    * No tan abstractos como patrones de diseño
    * No incluyen detalles de implementación
    * Agnósticos a lenguajes de programación
* Patrones deben poder incluir otros patrones (nesting)
* Herramientas básicas de trabajo también en multi-computing

![Patrones de procesamiento](image.png)


# Multhreadig vs multiprocessing vd Multi-computing

* Multithreading: 
    * Un solo proceso
    * Comparten memoria -- Se pueden comunicar muy facilmente, pero esto también puede ser un problema
    * Comunicación entre threads
    * Sincronización
    * No se puede escalar a multiples computadoras



* Multiprocessing:
    * Multiples procesos
    * No comparten memoria
    * Comunicación entre procesos
    * Sincronización
    * Se puede escalar a multiples computadoras


* Multi-computing:
    * Multiples computadoras
    * No comparten memoria
    * Comunicación entre computadoras
    * Sincronización
    * Se puede escalar a multiples computadoras





# Muchos procesadores(taxonomia de Flynn)

* SISD: Single Instruction Single Data: Un solo procesador, un solo dato. No hay parallelismo.
* SIMD: Single Instruction Multiple Data: Un solo procesador, muchos datos.
* MISD: Multiple Instruction Single Data: Multiples procesadores, un solo dato. No son usuales. Se suele usar por ejemplo en sistemas de redundancia y datapipelines.
* MIMD: Multiple Instruction Multiple Data: Multiples procesadores, muchos datos. Es el caso más natural.

    * Multiprocessorrs: Con memeoira y/p clock compartidos
    * completar ...



## Multiprocessors(Memoria comppartida)

![tipos de multiprocesos](image-1.png)

 ### MIMD - Multiprocessors - NUMA 

* Non-Uniform Memory Access
* Cada CPU controla un bloque de memeoraia local como su home agent 

COMPLETAR 


### MIMD - Multiprocessors - UMA


## Multicomputing




# Documentación Técnica y Diagramas

## Documentación 

La arquitectura representa aquellas decisiones de importancia, medidas de acuerdo al costo de modificarlas.

Diseño y documentación: 

* Evolutivo:
    * Adaptarse rapido, tomar feedback y aportar alor iterativamente.
    * No buscar el entendimiento del todo y ni domorar la arquitectura.

* Necesario para la coodinación, coherncia y cohesión.
    * Sin un diseño preliminar, probablemente jamás haya diseño.


Framework de documentación:

* Vista de Arquitectura 4+1

    ![Arquitectura 4+1](image-2.png)

### Contenido de la documentación

1. 


# Nobmbres y direcciones 

* Nombres
    * Permiten identificar unívocamente a una entidad dentro de un sistema
    * Deben describir a la entidad
    * Abstraen al recurso de las propiedades que atan al mismo con el sistema (lugar geográfico, direcciones de red)
* Direccionamiento (Addressing)
    * Mapeo entre un nombre y una dirección
    * Dirección de una entidad puede cambiar, nombre no (*)
    * Dirección puede ser reutilizada


## Ejemplos 

* Domain Name (name) -> IP Address (address)
    * Mapeo de un servicio/nodo/otra entidad a una dirección IP
    * Traducción a través de protocolo DNS

![alt text](image-3.png)

Probar el comando dig y analzar la respuesta.




* IP Address (name) -> Ethernet Address (address)
    * IP address identifica a un nodo en un red (sea local o no)
    * Ethernet address identifica a NIC (network interface card) de un nodo
en una red local 
    * Resolución se realiza a través de protocolo ARP en IPv4 o ND
(Neighbor Discovery) en IPv6
* Service (name) -> Instances (address)
    * Mapeo del nombre de un servicio a alguna instancia
    * Resolución a través de Service Discovery(buscar un poco más acerca del tema )
    * Diferentes implementaciones existentes: Zookeeper, Istio, Linkerd


![alt text](image-4.png)

Lo que se hace en este caso es para servicios privados de la misma empresa, Puede servir para cuando se cae un servicio privado, lo que hago es redirigir a otro servicio que esté funcionando. O puede estar el caso en el que quiero que haya veces que vaya hacia un servicio o hacia otro.

*QUIERO SABER PORQUE NO USAR DNS PARA ESTO*
