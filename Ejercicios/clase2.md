## Ejercicio IPC Rendezvous

- N threads/procesos deben generar M mensajes
- Cada thread/proceso genera un mensaje y espera a que sus pares terminen de hacer lo mismo
- Cuando todos los threads/procesos hayan terminado de generar una ronda de mensajes procederán a generar uno nuevo
- Resolver utilizando IPCs
  - Shared Memory / Semaphores
  - Message Queues

## Ejercicio Sicronización Rendezvous

- N threads/procesos deben ejecutar M tareas
- Cada thread/proceso ejecuta su tarea y espera a que sus pares terminen de hacer lo mismo
- Cuando todos los threads/procesos hayan terminado de ejecutar una ronda de tareas, proceden a ejecutar una nueva ronda
- Resolver utilizando la abstracción BlockingQueue

## Ejercicio Barrera

- N threads/procesos deben ejecutar M tareas
- Cada thread/proceso ejecuta su tarea y espera a que sus pares terminen de hacer lo mismo
- Cuando todos los threads/procesos hayan terminado de ejecutar una ronda de tareas, proceden a ejecutar una nueva ronda
