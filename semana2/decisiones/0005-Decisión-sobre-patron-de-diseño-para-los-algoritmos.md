# Decisión sobre patron de diseño para los algoritmos

* Status: accepted
* Deciders: ASS
* Date: 2024-11-06

Technical Story: Se va a decidir sobre la manera en la que se organizarán los algoritmos

## Context and Problem Statement

Debido a nuestras necesidades de desarollo, tenemos que elegir como diseñar de manera eficiente la organización y elección de nuestros dos algoritmos de enrutamiento de los reparotos de pedidos. Debemos valorar diversas opciones

## Decision Drivers

* RF- 6 Seleccion de algoritmos de optimizacion de reparto

## Considered Options

* Patrón Estrategia
* Patrón Comando
* Patrón de Plantilla

## Decision Outcome

Chosen option: "Patrón Estrategia", because permite definir una familia de algoritmos de reparto que pueden ser intercambiados de manera flexible.

### Positive Consequences

* Si necesitas añadir nuevos algoritmos o modificar los existentes, puedes hacerlo sin afectar a la clase principal ni a otros algoritmos. Esto facilita la evolución y escalabilidad de la aplicación.
* Puedes cambiar de estrategia en tiempo de ejecución, seleccionando la más adecuada según las necesidades actuales, como el tráfico o las preferencias del cliente. Esto es especialmente útil en sistemas de rutas donde la elección óptima de algoritmo puede depender de factores externos.
* Al separar los algoritmos en clases específicas, puedes reutilizar el mismo código en otras partes de la aplicación si hay módulos que también necesitan realizar cálculos de rutas. Cada algoritmo encapsulado puede ser utilizado por diferentes clases sin duplicar código.

### Negative Consequences

* Dado que necesitas una instancia del algoritmo adecuado para cada situación, el patrón puede requerir un gestor de configuración adicional o una fábrica para seleccionar el algoritmo apropiado. Esto introduce algo de complejidad en la configuración de la aplicación.
* Si los algoritmos de reparto tienen partes del código en común, podría haber duplicación en las implementaciones de cada estrategia. En estos casos, el Patrón de Plantilla (Template Method) podría ser más eficiente, ya que permite que las subclases compartan un flujo general con solo pasos específicos sobrescritos.
* Cada nuevo algoritmo requiere una nueva clase, lo que puede aumentar la complejidad del proyecto en términos de estructura de archivos. En sistemas grandes, este incremento puede hacer que el código sea más difícil de navegar y gestionar.

## Pros and Cons of the Options

### Patrón Estrategia

El Patrón Estrategia permite definir una familia de algoritmos, encapsular cada uno en una clase separada e intercambiarlos de manera flexible. Se utiliza cuando necesitas que una clase realice una tarea de múltiples maneras (por ejemplo, diferentes algoritmos de reparto) y deseas poder seleccionar el algoritmo específico en tiempo de ejecución.

* Good, because Permite añadir o cambiar algoritmos sin modificar el código que los usa, facilitando la evolución del sistema.
* Good, because Puedes intercambiar las estrategias en tiempo de ejecución, ideal cuando tienes múltiples algoritmos que el sistema selecciona dinámicamente.
* Good, because Cada algoritmo de reparto está en su propia clase, manteniendo el código bien organizado y reduciendo dependencias.
* Bad, because En aplicaciones más grandes, gestionar y configurar diferentes estrategias puede añadir complejidad, sobre todo si existen muchas variantes.
* Bad, because Si el número de estrategias crece, también crece el número de clases, lo que puede hacer el proyecto más difícil de manejar.
* Bad, because Cuando necesitas que los algoritmos sigan un flujo específico, este patrón no es el mejor, ya que cada estrategia opera de manera independiente.

### Patrón Comando

El Patrón Comando encapsula una operación o solicitud como un objeto, lo que permite parametrizar acciones, almacenarlas en una cola, registrar un historial, o deshacerlas fácilmente. Es útil cuando quieres ejecutar, deshacer o almacenar acciones sin conocer sus detalles internos

* Good, because Permite que el código que solicita una operación no necesite saber cómo se implementa, lo que es útil en sistemas modulares y complejos.
* Good, because Al encapsular las operaciones en objetos, puedes almacenarlas y crear un historial. Esto es útil si deseas tener la capacidad de registrar y deshacer operaciones.
* Good, because Puedes diferir la ejecución, ejecutar comandos en cola, y combinarlos en operaciones más complejas (como una cadena de comandos o "macro-comandos").
* Bad, because Similar al Patrón Estrategia, cada comando es una clase independiente. En sistemas complejos, esto puede incrementar la cantidad de clases de manera significativa.
* Bad, because Si el historial o deshacer de operaciones no es un requisito, el Patrón Comando puede añadir complejidad innecesaria.
* Bad, because Para operaciones simples o directas, encapsular cada acción en un comando puede ser excesivo, añadiendo capas de abstracción innecesarias.

### Patrón de Plantilla

El Patrón de Plantilla define el esqueleto de un algoritmo en una clase base, dejando ciertos pasos específicos a subclases. Se utiliza cuando tienes un flujo o secuencia de pasos común que varias implementaciones necesitan seguir, pero algunos pasos específicos varían

* Good, because Permite que las subclases compartan la estructura y los pasos comunes de un algoritmo, reduciendo duplicación y facilitando el mantenimiento.
* Good, because Útil cuando tienes un flujo predefinido y solo ciertos pasos varían, lo que asegura que las operaciones sigan un esquema común.
* Good, because Permite añadir nuevos pasos o algoritmos que aprovechan la estructura general sin cambiar la lógica base del flujo.
* Bad, because Los métodos específicos se determinan en tiempo de compilación, por lo que no es posible cambiar el comportamiento en tiempo de ejecución como en el Patrón Estrategia.
* Bad, because Si las variaciones en el flujo son complejas o existen múltiples puntos de variación, este patrón puede volverse confuso y difícil de manejar.
* Bad, because Las subclases dependen de la estructura de la clase base, lo que reduce la independencia de cada implementación y limita la flexibilidad para modificaciones significativas en el flujo.

## Links

* RF- 6 Seleccion de algoritmos de optimizacion de reparto
