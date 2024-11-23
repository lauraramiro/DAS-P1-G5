# Decisión-sobre-módulo-de-estadística

* Status: accepted
* Date: 2024-11-20

Technical Story: Se decidira sobre como realizar el módulo de estadistica

## Context and Problem Statement

Se necesita en nuestro programa un módulo gestor de estadísticas de nuestros clientes y la manera de hacerla.

## Decision Drivers

* RF-9 Módulo de estadísticas

## Considered Options

* Crear una clase base
* Clase estática
* Interfaz funcional con clases anónimas

## Decision Outcome

Chosen option: "Crear una clase base", because nos conviene en mayor medida comparado con el resto de propuestas

### Positive Consequences

* Ayuda a mantener el código limpio y modular, especialmente en proyectos grandes o de mediana escala.
* Ahorra tiempo en futuros desarrollos y mejora la consistencia en la aplicación.

### Negative Consequences

* Implementar una clase dedicada puede requerir más esfuerzo inicial, especialmente si el diseño incluye muchos métodos o funcionalidades.

## Pros and Cons of the Options

### Crear una clase base

Se crearía una clase para gestionar todas las estadísticas y conectarla a los elementos correspondientes.

* Good, because Todo el código relacionado con estadísticas está en un solo lugar, facilitando su mantenimiento.
* Good, because Se puede usar en diferentes proyectos con pocos cambios.
* Good, because Es fácil agregar nuevos métodos estadísticos o modificar los existentes sin afectar el resto del programa.
* Bad, because Puede ser excesivo si el proyecto es pequeño.
* Bad, because Si creas múltiples instancias de la clase innecesariamente.

### Clase estática

En lugar de crear una clase con objetos instanciables, puedes usar una clase que contenga solo métodos estáticos. Esto permite que las funciones estadísticas se llamen directamente desde la clase sin necesidad de crear instancias.

* Good, because No necesitas manejar el ciclo de vida de los objetos; solo se invocan métodos estáticos.
* Good, because Cualquier parte del código puede usar estas funciones sin pasar por la creación de instancias.
* Bad, because Si necesitas agregar estados o propiedades específicas, los métodos estáticos no lo permiten fácilmente.
* Bad, because Puede ser difícil reutilizar el código en arquitecturas orientadas a objetos complejas.

### Interfaz funcional con clases anónimas

Define una interfaz funcional que represente una operación estadística. Luego, puedes implementar cálculos específicos mediante expresiones lambda o clases anónimas.

* Good, because Puedes definir y personalizar fácilmente nuevas operaciones estadísticas.
* Good, because Las operaciones son independientes unas de otras.
* Good, because Aprovecha características modernas de Java como expresiones lambda y Streams.
* Bad, because Requiere un diseño más abstracto, lo cual puede ser innecesario en proyectos simples.

## Links

* RF-9 Módulo de estadísticas
