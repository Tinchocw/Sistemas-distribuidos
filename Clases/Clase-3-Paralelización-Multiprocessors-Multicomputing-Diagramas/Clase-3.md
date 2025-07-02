# Clase 3 - Paralelización, Multiprocessors, Multicomputing

## Paralelización de tareas: Introducción

- Objetivos:

  - Reducir el tiempo de computo de una tarea(latencia).
  - Aumentar la cantidad de tareas que se pueden realizar en paralelo (throughput).
  - Reducir la energia consumida al realizar todas las tareas.

- Camino critico:
  - Maxima longitud de tareas secuenciales a computar.
  - Define el mejor rendimiento que se puede obtener al ejecutar un conjunto de tareas.

## Paralelización de tareas: Ley de Amdahl

Tengo tareas, una parte es paralelizable y la otra es serial(esto si o si va a estar).

![alt text](image-2.png)

Siendo f la fracción de tiempo en la que se ejecuta la parte serial y 1-f la fracción de tiempo en la que se ejecuta la parte paralelizable.

La idea es que si yo tengo un solo procesador, lo que hago es hacer primero la parte serial y despues la parte paralelizable, en cambio, en el caso de tener más de un procesador lo que se hace es dejar la parte serial en un procesador y despues el paralelizable lo separo en los demas procesadores.

- Peor caso: Lo maximo que puedo tardar es si tengo un solo procesador.
- Mejor caso: Que pasa si tenog infinita paralelización, lo mejor que puedo lograr sería ... (ver en la clase).

Si tengo P unidades de computo, el tiempo total de computo puede reducirse:

![alt text](image-13.png)

Lo que busco en este caso es dividir el computo entre las P unidades de computo que tengo, y la parte serial la voy a tener que hacer en una sola unidad de computo.

Aparece un nuevo concepto llamado "speedup" que se define como el ratio de la optimización de una operación.

```
Sp = T1 / Tp

- reemplazando

--> Sp <= 1 / f + (1 - f) / P

- con P -> infinito

--> Sp <= 1 / f
```

Entonces la conclusión a la que llegamos es que el speedup máximo se encuentra acotado "por la fracción de tiempo que no puede ser paralelizada".

## Ley de Gustafson

El speedup no debes medirlo con una unica tarea sino que deberias medirlo escalando el problema.

## Modelo work-span

- Caracteristicas
  - Modelo más cercano a la realidad para estimar optimizaciones que el usado por Amdahl
  - Provee una cota inferior y una cota superior para el Speedup
- Hipótesis
  - Paralelismo Imperfecto: No todo el trabajo paralelizable se puede ejecutar al mismo tiempo
  - Greedy scheduling: proceso disponible => tarea ejecutada
  - Tiempo de acceso a memoria despreciable
  - Tiempo de comunicación entre procesos despreciable
  - Posibilidad de analizar la operación/algoritmo en caja blanca

### Paralización de tareas

- Definiciones

  - T1 (work): Tiempo en ejecutar "operación/algoritmo" con 1 sólo proceso
  - Tinf (span): Tiempo en ejecutar el camino crítico de la "operación/algoritmo"

  ![alt text](image-14.png)

  ### Ejemplo practico de la implementación de Work y Span

  ![alt text](image-15.png)

  ### Comparación entre Amdahl y Work-Span

  ![alt text](image-16.png)

## Estrategia de paralelización

Descomposición funcional: Tengo una fución con tres dentro funciones dentro de la misma. Lo que hago es poder paralelizar la funciones que tengo dentro de la misma

Particionamiento de datos: Los datos se deben poder separar, la función se pueda separar. La idea es separar los datos para poder paralelizar, se va a hacer un fork y un join en algun momento.

## Patrones de procesamiento

- Basados en algoritmos
  - No tan abstractos como patrones de diseño
  - No incluyen detalles de implementación
  - Agnósticos a lenguajes de programación
- Patrones deben poder incluir otros patrones (nesting)
- Herramientas básicas de trabajo también en multi-computing

<img src="image.png" alt="alt text" width="700">

# Multhreadig vs multiprocessing vd Multi-computing

- Multithreading:

  - Un solo proceso
  - Comparten memoria -- Se pueden comunicar muy facilmente, pero esto también puede ser un problema
  - Comunicación entre threads
  - Sincronización
  - No se puede escalar a multiples computadoras

- Multiprocessing:

  - Multiples procesos
  - No comparten memoria
  - Comunicación entre procesos
  - Sincronización
  - Se puede escalar a multiples computadoras

- Multi-computing:
  - Multiples computadoras
  - No comparten memoria
  - Comunicación entre computadoras
  - Sincronización
  - Se puede escalar a multiples computadoras

# Muchos procesadores(taxonomia de Flynn)

- SISD: Single Instruction Single Data: Un solo procesador, un solo dato. No hay parallelismo.
- SIMD: Single Instruction Multiple Data: Un solo procesador, muchos datos.

![alt text](image-17.png)

- MISD: Multiple Instruction Single Data: Multiples procesadores, un solo dato. No son usuales. Se suele usar por ejemplo en sistemas de redundancia y datapipelines.
- MIMD: Multiple Instruction Multiple Data: Multiples procesadores, muchos datos. Es el caso más natural.

  - Multiprocessorrs: Con memeoira y/p clock compartidos
  - Multicomputers: sin memoria ni clock compartidos

![alt text](image-18.png)

## Multiprocessors(Memoria compartida)

<img src="image-1.png" alt="alt text" width="700">

### MIMD - Multiprocessors - NUMA

- Non-Uniform Memory Access
  - Cada CPU controla un bloque de memoria local como su home agent
  - Mayor ancho de banda si se respeta el acceso a memoria local.
  - Ideado en SGI, presente en Linux kernel y MS Servers.
  - Luego de años en desuso, nuevamente se ofrece en Cloud (ver Ej.)

### MIMD - Multiprocessors - UMA

- Uniform Memory Access (UMA == non-NUMA)

  - Tiempo de acceso a la memoria es idéntico para todos los procesadores.
  - Ancho de banda compartido por todos.
  - Performance balanceada para aplicaciones de uso general

## Multicomputing - sin memoria compartida

- Cada computadora tiene su propia memoria local
- Cada computadora puede fallar de forma independiente
- No poseen un reloj central de ejecución de instrucciones
- Requieren comunicación entre computadoras:
  - Networking: LAN, MAN, WAN

# Nombres y direcciones

- Nombres
  - Permiten identificar unívocamente a una entidad dentro de un sistema
  - Deben describir a la entidad
  - Abstraen al recurso de las propiedades que atan al mismo con el sistema (lugar geográfico, direcciones de red)
- Direccionamiento (Addressing)
  - Mapeo entre un nombre y una dirección
  - Dirección de una entidad puede cambiar, nombre no (\*)
  - Dirección puede ser reutilizada

## Ejemplos

- Domain Name (name) -> IP Address (address)
  - Mapeo de un servicio/nodo/otra entidad a una dirección IP
  - Traducción a través de protocolo DNS

![alt text](image-3.png)

Probar el comando dig y analzar la respuesta.

- IP Address (name) -> Ethernet Address (address)
  - IP address identifica a un nodo en un red (sea local o no)
  - Ethernet address identifica a NIC (network interface card) de un nodo en una red local
  - Resolución se realiza a través de protocolo ARP en IPv4 o ND
    (Neighbor Discovery) en IPv6
- Service (name) -> Instances (address)
  - Mapeo del nombre de un servicio a alguna instancia
  - Resolución a través de Service Discovery
  - Diferentes implementaciones existentes: Zookeeper, Istio, Linkerd

![alt text](image-4.png)

El cliente solo envía la solicitud a un proxy o balanceador de carga, y este se encarga de encontrar el servicio adecuado.

1. El cliente envía una solicitud a un endpoint fijo (como un balanceador de carga o proxy).

2. El balanceador consulta el registro de servicios y elige la mejor instancia disponible.

3. El balanceador reenvía la solicitud a la instancia correcta.

### Ejemplos:

### Escenario 1: Failover Automático entre Servicios Internos

#### Caso de Uso

Una empresa tiene un sistema interno de autenticación (auth-service) que permite a los empleados iniciar sesión en sus aplicaciones. Hay dos instancias de este servicio corriendo en distintas regiones:

- auth-service-us
- auth-service-eu

Si auth-service-us falla, el tráfico debe redirigirse automáticamente a auth-service-eu sin intervención manual.

Solución con Service Discovery (Ejemplo con Consul)
Con Consul (u otra herramienta de Service Discovery como Kubernetes o AWS Cloud Map), los servicios pueden registrarse dinámicamente y hacer failover sin depender de DNS.

### Escenario 2: Redirección de Tráfico según Condiciones (A/B Testing o Canaries)

#### Caso de Uso

Una empresa está lanzando una nueva versión de su servicio de facturación (billing-service). Quieren que solo el 20% de los usuarios sean redirigidos a la nueva versión (billing-service-v2), mientras que el resto siga usando la versión estable (billing-service-v1).

### Razones para usar Server-Side Discovery en lugar de DNS

1. DNS NO SE ACTUALIZA EN TIEMPO REAL (TTL)

   **Problema**:

   Cuando un servicio cambia de dirección IP (por ejemplo, si un contenedor se reinicia en Kubernetes), los cambios en DNS tardan en propagarse debido al TTL (Time To Live) configurado en los registros DNS.

   **Ejemplo**:

   1. service-a llama a service-b en service-b.mycompany.com (con DNS).

   2. service-b se mueve a otra IP.

   - DNS tarda varios minutos en actualizarse -- service-a sigue llamando a la IP vieja y falla la comunicación.

   - Con Service Discovery en el lado del servidor (ejemplo con Kubernetes):

     - Kubernetes maneja automáticamente los cambios de IP sin depender de DNS.

     - service-a sigue llamando a service-b y el tráfico siempre llega a una instancia válida.

2. DNS NO BALANCEA EL TRÁFICO DE FORMA INTELIGENTE
   **Problema**:
   DNS puede balancear tráfico con Round-Robin DNS, pero no tiene en cuenta el estado real de los servidores.

   **Ejemplo**:

   Tienes dos servidores para payment-service:

   - server-1 (IP: 10.0.1.1)
   - server-2 (IP: 10.0.1.2)

   DNS responde con ambas IPs de forma aleatoria. --- Si server-1 se cae, DNS no lo sabe y los clientes pueden seguir intentando conectarse a él.

   Con Server-Side Discovery un balanceador de carga o proxy detecta automáticamente qué instancias están vivas y solo envía tráfico a las saludables.
   Se pueden aplicar reglas avanzadas, como:

   - Enviar tráfico a instancias con menos carga.

   - Evitar servidores con alta latencia.

   - Hacer "circuit breaking" si un servicio falla muchas veces seguidas.
