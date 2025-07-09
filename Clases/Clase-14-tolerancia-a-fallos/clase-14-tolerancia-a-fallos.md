# Tolerancia a fallos 


## Resiliencia | Safety

El sistem debe poder ser recuperdao automáticamente o manualmente ante cuaquier tipo de falla.


Uno tinene que garantizar el tiempo de maintinability y la 

## Consenso

Procedimiento que para que un conjunto de procesos distribuidos acuerden en el mismo valor dado un punto de decisión compartido,

Implica la coordinación y un algotirmo de acuerdo.


Hay que tomar algunas condiciones para que el consenso sea posible:

Un ejemplo puede ser:

* Tengo que ver si los canales de comunicación son fiables o no.
* Todos los procesos pueden comunicarse entre sí
* Única falla a considerar es la caída de un proceso.
* Caída de un proceso no puede ocasionar la caída de otro proceso.

## Coordinación y acuerdo


### Ej: 
El valor que sabía P1 sea comunicado a P2 y P3, y el valor que sabía P2 sea comunicado a P1 y P3, y el valor que sabía P3 sea comunicado a P1 y P2.

Luego de ciertos pasos todos van a tener una tupla que va a tener los valores de los otros procesos. Y lo que podemos hacer en este caso es que me de la mayoría de los valores. Y así se llega a un consenso.



## Casos de consenso

### Exclusión mutua distribuida

#### Servidor central 

Un servidor central es un proceso que se encarga de coordinar el acceso a un recurso compartido entre varios procesos. Este servidor central es responsable de recibir las solicitudes de acceso al recurso, otorgar permisos y garantizar que solo un proceso tenga acceso al recurso en un momento dado.




## Algoritmos de consenso



## Paxos


Objetivo: Cones




