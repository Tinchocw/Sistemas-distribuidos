# Clase 9 

## Escalabilidad

El objetivo es el crecimiento. 
* En en usuarios o recursos a controlar. 
* Pero tambíen puedo crecer de forma geografiaca(tengo nuevos usuarios que provienen de disttintos lugares ¿).


## Caracteristicas de la plataforma 

No siempre sirve con poner más computadoras.

* Plataformas de alta concurrencia
    * Aplicar en patrones ya conocidos y probados
    * Escalamiento automatico -- Se puede setear algunos limites -- 
    * Vinculación fuerte con una infraestructura    



* Arquitecturas Ad-Hoc y personalizadas 
    * Necesidad de configuración y soporte 
    * Escalamiento manual o automatizado por humanos 
    * Posibilidad de migraciones a distintas plataformas() --- si tengo un sistema de tiendas y lo que hago es subirme a una aplicación para que me de más computo. Puede pasar la situación en la que mi sistema quede atado a una plataforma de cloud, esto no es la idea.


Se busca no tener un "vendor loc" (buscar que es).


## Patrones de carga de aplicaciones web

* Predictable Burst: En este caso es cuando se que va a venir una subida de peticiones, se que viene y puedo actuar al respecto(puedo comprar más maquinas, alquilarlas temporalmente o más cloud para esta situación)
* Unpredictable Burst: No se en que momento van a estar las subidas de peticiones.
* Periodic processing: El caso de una banco, de la bolsa. Ver bien
* Start Small. Groe Fast: 


A cuanta capacidad tiene que estar un servidor? La idea es que depende de como es el comportamiento que recibe normalmente. Si yo se que es predecible y siempre es el mismo busco usar la mayor capacidad dejando siempre un margen para imprevistos. Pero en el caso que yo se que tengo comportamiento impredecible va a pasar que si tengo el servidor utilizandolo cerca del 100% no voy a poder llevar adelante esta subida de recursos a utilizar para cumplir lo esperado.



## Limitaciones

Los canales por los que estas intercambiando mensajes tienen la latencia esperada? 
Ancho de banda -- capacidad de información que puedo enviar en paralelo

* Arquitecturas y algoritmos
* Red (ancho de banda)
* Restricciones legales uy de negocio: Ej: Redistribución de datos medicos. Son sensibles y no se pueden estar pasando porque si. Un caso puede ser que un usuario se va de viaje y tiene un accidente en otro país, entonces yo quiero pasasr la información medica del usuario de antemano para evitar la latencia, pero esto no se puede hacer justamente porque no se puede estar compartiendo libremente este tipo de información.



## Tecnicas 

* Escalamiento vertical: Agregar recursos a un nodo. Más RAM.
* Escalamiento horizontal: Más nodos.
    * Se necesita redundancia
    * Proximidad geografica -- siempre esta la información donde se necesita, puedo encofar a los recursos en donde más lo necesito.
    * Balanceamento de cargas

* Optimización de algoritmos(cuando estoy dentro de una misma computadoras)
    * Performance 
    * Mesajeria -- Resuelvo bien las consultas, no envio mensajes de forma innecesaria. Buena coordinación de mensajes.

* Fragmentación de los datos
    * Fraccionar para optimizar -- pasar la información necesaria solo a los nodos que la requieren
    * Manetener juntos datos "cargados"

* Asincronismo
    * Mantener sincronico unicamente lo estrictamente necesario
    * Limitado por el negocio



## Elasticidad

Tener en cuenta en modificar dinamicamente los recursos del sistema para adaptarse a patrones de carga. Me viene 3 usuarios más y lo que quiero es escalar lo más rapido posible en un tiempo razonable para poder procesar la información.


### Componentes

* Load balance: El reporte de cada nodo lo hace el mismo, pero el encargado del reporte de todo el sistema es el middleware.


VER LA DIAPO Y EJEMPLO DE AWS


## Alta disponibilidad 

No se puede tener probabilidad 1 de estar disponible.

La disponibilidad de un sistema se mide por la canitdad de 9's. Siendo la probabilidad 0.9, 0.99 y así. Siempre que tenga más 9 va a estar mejor.


 ## CAP Theorem 

 En sistemas distribuidos con almacenamiento es posibe garantizar solo 2 de los sigiuente atributos 

  COMPLETAR 


    








  


