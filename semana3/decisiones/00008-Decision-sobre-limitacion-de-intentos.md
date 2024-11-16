# Decision sobre limitacion de intentos

* Status: proposed
* Date: 2024-11-16

Technical Story: Se va a discutir como se eligirá el limitador de intentos en los pedidos

## Context and Problem Statement

Se necesita decidir hacer una limitación en los pedidos, mas especificamente en el numero de pedidos que se puede hacer.

## Decision Drivers

* RF-5-1 Limitación modulo pedidos

## Considered Options

* Patrón retry
* Contador manual de intentos

## Decision Outcome

Chosen option: "Pátron retry", because creemos que la manera mas internacionalmente estandarizada y correcta es la del uso de este patron para nuestras necesidades.

### Positive Consequences

* El sistema puede tolerar fallos temporales sin interrumpir completamente el flujo de ejecución, especialmente útil en operaciones críticas
* La lógica de reintentos queda encapsulada, lo que permite aplicarla fácilmente en diferentes partes del sistema sin duplicar código.
* Puedes adaptar la estrategia de reintentos según las necesidades

### Negative Consequences

* Implementar y mantener el patrón Retry, especialmente con estrategias avanzadas como el retroceso exponencial, requiere más diseño y pruebas.
* Configurar incorrectamente el número de intentos, el tiempo de espera, o las excepciones manejadas puede llevar a bucles infinitos o fallas no controladas.

## Pros and Cons of the Options

### Pátron retry

El patrón Retry encapsula la lógica de reintentos en un mecanismo centralizado. Se intenta ejecutar una operación un número limitado de veces, con posibles pausas entre intentos.

* Good, because Permite reutilizar la lógica de reintentos en varias partes del sistema.
* Good, because Soporta diferentes estrategias de reintento (exponencial, constante, etc.).
* Good, because Mejora la tolerancia a fallos temporales sin bloquear permanentemente el sistema
* Bad, because Requiere más código y diseño inicial.
* Bad, because Mal configurado, puede causar reintentos excesivos si no se limita adecuadamente.

### Contador manual de intentos

Se mantiene un contador en el contexto donde se realiza la operación. Se intenta la operación, incrementando el contador en cada intento, hasta alcanzar el límite máximo de reintentos.

* Good, because Fácil de implementar y entender.
* Good, because La lógica de reintentos se encuentra explícitamente en el flujo del programa.
* Bad, because Si se utiliza en varios lugares, la lógica puede repetirse y volverse difícil de mantener.
* Bad, because Menos configurable para estrategias avanzadas como retroceso exponencial o manejo de excepciones.

## Links

* RF-5-1 Limitación módulo pedidos
