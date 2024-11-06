# Decisión sobre el desacoplamiento de rutas y reparto

* Status: accepted
* Deciders: ASS
* Date: 2024-11-06

Technical Story: Se decide sobre el tipo desacoplamiento de las rutas y el reparto

## Context and Problem Statement

Necesitamos desacoplar las rutas del reparto en nuestro diseño de la nueva version de nuestra app. Para hacer esto hemos considerado dos opciones sobre las que ponderar el tipo de estructura final

## Decision Drivers

* RF-7 Desacoplar módulos de reparto y rutas

## Considered Options

* Creación de una clase organizadora con métodos separados
* Separación de rutas y repartos en clases inpendientes

## Decision Outcome

Chosen option: "Separación de rutas y repartos en clases inpendientes", because creemos que esta opcion se alinea más con la politica de desacoplamiento

### Positive Consequences

* Al separar rutas y repartos, cada clase es más sencilla de entender y modificar individualmente. Esto facilita localizar y corregir errores o realizar actualizaciones sin afectar a la otra clase.
* La arquitectura modular permite que cada funcionalidad crezca y evolucione de forma independiente. Si se necesitan nuevos métodos o mejoras específicas en rutas o repartos, se pueden añadir sin impactar a toda la aplicación.
* Cada clase se puede probar de forma independiente. Esto facilita la creación de pruebas unitarias específicas y la detección de errores en cada módulo, mejorando la calidad del software.

### Negative Consequences

* Dado que las clases están desacopladas, asegurarse de que ambas tengan la información actualizada en tiempo real puede ser complicado, sobre todo si se manejan datos de forma asincrónica o distribuida. Esto podría requerir mecanismos adicionales para mantener la sincronización entre ambas.

* La comunicación entre dos clases diferentes puede tener un coste de rendimiento, especialmente si estas clases interactúan frecuentemente o si la arquitectura de comunicación es pesada (por ejemplo, con llamadas de red en lugar de en memoria).
* Puede surgir la necesidad de implementar una clase o módulo adicional que gestione la interacción entre rutas y repartos, lo cual agrega otra capa de complejidad y, potencialmente, más código que mantener.

## Pros and Cons of the Options

### Creación de una clase organizadora con métodos separados

Se ha pensado crear una clase que aglomera a las rutas y los repartos. Esta clase usaría métodos separados para la organización de las rutas y los repartos

* Good, because Centralizar ambas funcionalidades en una sola clase es más sencillo de implementar al inicio.
* Good, because Si la lógica de rutas y repartos está muy ligada entre sí, tener una sola clase puede hacer que el código sea más fácil de seguir y entender..
* Good, because Al estar en la misma clase, se facilita la transferencia de datos entre rutas y repartos, eliminando la necesidad de crear un mecanismo de comunicación entre dos clases.
* Bad, because Las funcionalidades están unidas, lo que puede dificultar el mantenimiento y la escalabilidad. Si necesitas cambiar una funcionalidad, puede impactar en la otra.
* Bad, because La clase puede volverse demasiado compleja, tratando de manejar la lógica de rutas y de repartos al mismo tiempo.
* Bad, because Las pruebas pueden ser más complicadas porque la clase tiene múltiples responsabilidades, lo que puede generar dependencias difíciles de manejar en un entorno de testing.

### Separación de rutas y repartos en clases inpendientes

Se separarían las rutas y los repartos en clases independientes. Estas clases manejarían de manera autonoma los divesos aspectos de ambas.

* Good, because Cada clase se centra en su función específica, lo que facilita mantener y modificar su lógica sin afectar a la otra.
* Good, because Las clases pueden ser reutilizadas en diferentes partes del sistema u otros proyectos si es necesario.
* Good, because Facilita realizar pruebas unitarias, ya que las dependencias están limitadas y cada clase puede ser testeada por separado.
* Bad, because Implica un diseño más complejo al principio, especialmente si se requiere manejar muchos datos entre ambas.
* Bad, because Necesitarás implementar un mecanismo para que ambas clases se comuniquen y compartan la información necesaria, como rutas asignadas a los repartos.

## Links

* RF-7 Desacoplar módulos de reparto y rutas
