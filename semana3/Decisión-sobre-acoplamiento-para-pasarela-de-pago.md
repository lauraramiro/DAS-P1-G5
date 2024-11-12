# Decisión sobre acoplamiento para pasarela de pago

* Status: accepted
* Deciders: ASS
* Date: 2024-11-12

Technical Story: Se decide como se diseñará la pasarela de pago

## Context and Problem Statement

Se necesita una pasarela de pago que ya se nos da hecha y debemos de incrustar en nuestros servicios. Dado esto necesitamos una manera o estrategia para incluir esto en nuestra apicación.

## Decision Drivers

* RF- 10 Acceso a la pasarela de pago

## Considered Options

* Patrón API Gateway
* Patrón Saga
* Patrón Circuit Breaker

## Decision Outcome

Chosen option: "Patrón API Gateway", because se adapta mas a nuestro ambiente y necesidad con las api.

### Positive Consequences

* La API Gateway permite gestionar la autenticación y autorización en un solo punto de acceso. Puedes aplicar políticas de seguridad, autenticación (por ejemplo, OAuth) y validación de permisos, protegiendo los servicios internos.
* Al tener un punto de entrada único, los clientes (por ejemplo, aplicaciones móviles o web) solo interactúan con el Gateway, sin necesidad de conocer o gestionar las complejidades de la arquitectura interna.
* La API Gateway puede balancear la carga entre instancias de microservicios, aplicar límites de tasa (rate limiting), y proteger el sistema contra picos de tráfico o ataques de denegación de servicio (DDoS).

### Negative Consequences

* La API Gateway centraliza el acceso a los servicios, por lo que si falla, el sistema completo podría quedar inaccesible.
* Al agregar una capa adicional entre el cliente y los microservicios, se incrementa la latencia en las solicitudes, ya que cada petición pasa por la Gateway antes de llegar al servicio final.
* La configuración de una API Gateway robusta requiere una administración adecuada de rutas, autenticación, balanceo de carga, límites de tasa, y más. Además, cualquier cambio en las rutas o microservicios debe actualizarse en la configuración de la Gateway.

## Pros and Cons of the Options

### Patrón API Gateway

Un API Gateway es un único punto de entrada para todas las solicitudes de clientes hacia los microservicios de tu sistema. Actúa como un intermediario que se encarga de la autenticación, enrutamiento y, a menudo, seguridad de las solicitudes.

* Good, because Los clientes interactúan solo con el Gateway, sin preocuparse por la estructura interna de los microservicios.
* Good, because Puedes gestionar autenticación, permisos y validaciones en un solo lugar.
* Good, because Puede limitar el número de solicitudes por usuario o por IP, ayudando a proteger los servicios de sobrecargas.
* Bad, because Si el Gateway falla, todo el sistema puede quedar inaccesible, por lo que suele requerir alta disponibilidad y monitoreo.
* Bad, because Introduce una capa adicional, lo que puede aumentar la latencia en las solicitudes.
* Bad, because Configurar y mantener un Gateway robusto requiere una administración adicional, especialmente con muchos microservicios.

### Patrón Saga

El patrón Saga divide una transacción distribuida en una serie de pasos o transacciones locales que se ejecutan en diferentes servicios. Cada paso es independiente y si alguno falla, la saga realiza "compensaciones" (acciones que revierten los pasos previos) para mantener la consistencia.

* Good, because Asegura que las transacciones complejas se completen correctamente o se reviertan sin dejar datos inconsistentes.
* Good, because En caso de errores, se puede ejecutar una lógica compensatoria que restablezca el sistema a su estado anterior.
* Good, because Permite que cada microservicio gestione su parte de la transacción de forma independiente, distribuyendo la carga.
* Bad, because La lógica de compensación y la gestión de cada paso puede ser compleja y requerir mucho desarrollo y pruebas.
* Bad, because Rastrear los estados en una transacción distribuida es difícil, ya que cada paso puede ocurrir en servicios y momentos distintos.
* Bad, because Dado que las compensaciones pueden ejecutarse después de un error, los datos podrían no estar siempre en su estado final de forma inmediata.

### Patrón Circuit Breaker

Este patrón protege los microservicios frente a caídas o tiempos de respuesta prolongados de servicios externos, como una pasarela de pago. Un Circuit Breaker supervisa las llamadas a estos servicios y bloquea las solicitudes después de detectar un número definido de errores consecutivos.

* Good, because Evita que un microservicio problemático o un servicio externo afecte al resto del sistema.
* Good, because Permite responder a fallos de manera controlada, evitando que los servicios se bloqueen en bucles de espera.
* Good, because Puede reintentar la conexión tras un tiempo, permitiendo una recuperación gradual del servicio.
* Bad, because Definir umbrales de error y tiempos de espera óptimos requiere un ajuste fino.
* Bad, because En sistemas muy dinámicos, un Circuit Breaker mal configurado puede bloquear servicios que solo presentan fallos temporales.
* Bad, because Cuando el circuito está abierto, los usuarios pueden recibir mensajes de error o tener que esperar a que el sistema reintente el servicio fallido.
