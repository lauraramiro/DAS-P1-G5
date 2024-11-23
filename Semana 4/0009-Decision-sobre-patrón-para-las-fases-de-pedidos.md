# Decision sobre patrón para las fases de pedidos

* Status: accepted
* Date: 2024-11-20

Technical Story: Decision sobre las tres fases distintas de

## Context and Problem Statement

Se necesita decidir sobre como diseñar las tres fases distintas de los pedidos, en específico en la parte del diseño. Se está pensando en que patrónes nos pueden servir.

## Decision Drivers

* RF-5-2 Procesado en el Módulo Pedido

## Considered Options

* Patrón Chain of responsibility
* Patrón command

## Decision Outcome

Chosen option: "Patrón Chain of responsibility", because se acomoda nuestras necesidades de manera mas acorde.

### Positive Consequences

* Cada paso depende del éxito del paso anterior para continuar. Esto se alinea perfectamente con el patrón Chain of Responsibility, ya que cada paso maneja su parte y decide si pasa el control al siguiente.
* Cada fase del proceso (preprocesado, autorización, aceptación) se implementa como un manejador independiente, desacoplando la lógica de cada paso.
* Si en el futuro necesitas agregar más pasos o cambiar el orden, el patrón Chain of Responsibility lo permite sin modificar la estructura básica del flujo.

### Negative Consequences

* Cuando la cadena es larga o dinámica, puede ser complicado identificar dónde se detuvo el flujo o qué manejador falló.
* Aunque el patrón busca desacoplar responsabilidades, puede surgir un acoplamiento implícito porque cada manejador depende de que el siguiente esté correctamente implementado para continuar el flujo.

## Pros and Cons of the Options

### Patrón Chain of responsibility

Este patrón permite que una solicitud pase a través de una cadena de manejadores (handlers), donde cada uno decide si procesa la solicitud o la pasa al siguiente. Se utiliza cuando el flujo de procesamiento es secuencial y cada paso tiene la opción de manejar o delegar la tarea.

* Good, because Cada paso del proceso es independiente, lo que facilita su mantenimiento y modificación.
* Good, because Puedes añadir, eliminar o reordenar pasos en la cadena sin afectar al resto.
* Good, because Los manejadores pueden decidir si procesan la solicitud o la pasan al siguiente.
* Bad, because Si la cadena es larga o dinámica, puede ser difícil rastrear dónde ocurrió un error.
* Bad, because Requiere configurar correctamente la secuencia de manejadores.
* Bad, because Cada manejador decide si pasa la solicitud, lo que puede limitar personalizaciones más complejas.

### Patrón command

Este patrón encapsula cada paso del proceso como un objeto independiente (comando), que puede ejecutarse, deshacerse o almacenarse. Es útil cuando quieres representar acciones como unidades reutilizables e independientes.

* Good, because Cada comando es autónomo, lo que facilita su reutilización en diferentes contextos.
* Good, because Permite manejar el orden de ejecución desde un invocador central.
* Good, because Puedes ejecutar, cancelar o repetir comandos individualmente.
* Bad, because Introduce más clases y objetos, lo que puede complicar la implementación para casos simples.
* Bad, because Requiere un control explícito del orden de ejecución, lo que no es ideal para cadenas dependientes.
* Bad, because El flujo depende de cómo el invocador gestiona los comandos.

## Links

* RF-5-2 Procesado en el Módulo Pedido
