# Decisión sobre módulo gestor de incidencias

* Status: accepted
* Deciders: ASS
* Date: 2024-11-12

Technical Story: Se necesita decidir sobre la manera de gestionar incidencias

## Context and Problem Statement

Necesitamos una manera de diseñar nuestro modulo de gestión de incidencias para nuestras rutas. Para ello se deben de pensar diversos patrones de diseño que se acoplen a nuestra diseñar.

## Decision Drivers

* RF-11 Gestión de incidencias

## Considered Options

* Patrón Observer
* Patrón Bus de eventos
* Patrón mediador

## Decision Outcome

Chosen option: "Patrón Observer", because porque su especialidad es las mas indicada para la adaptacion del modulo gestor de incidencias.

### Positive Consequences

* Este desacoplamiento, aunque no total, es suficiente para aplicaciones donde la comunicación es simple y directa, lo cual simplifica tanto el diseño como la implementación.
* Observer es un patrón fácil de entender y directo de implementar, ideal para notificaciones básicas.
* En sistemas donde los cambios de estado son frecuentes y se necesita una reacción inmediata de los observadores, Observer permite enviar notificaciones directamente y sin demoras.

### Negative Consequences

* El sujeto debe gestionar la lista de observadores y conoce su existencia, lo que crea una relación directa y un acoplamiento parcial entre el sujeto y los observadores.
* A medida que aumenta el número de observadores, el sujeto necesita más recursos para gestionar y notificar a todos, lo cual puede ser ineficiente en sistemas grandes.
* Cuando los observadores modifican el estado del sujeto en respuesta a una notificación, puede generarse un bucle de retroalimentación o notificaciones innecesarias.

## Pros and Cons of the Options

### Patrón Observer

El patrón Observer permite que un objeto (el sujeto) mantenga una lista de observadores que desean ser notificados cada vez que ocurra un cambio de estado o un evento relevante. Cada vez que el estado del sujeto cambia, notifica automáticamente a todos los observadores registrados.

* Good, because Las clases observadoras no necesitan conocer la implementación del sujeto; solo se suscriben para recibir los avisos.
* Good, because Permite añadir o eliminar observadores dinámicamente en tiempo de ejecución, manteniendo flexibilidad.
* Good, because Es un patrón relativamente simple y directo de implementar en Java, usando listas o conjuntos para gestionar observadores.
* Bad, because Si hay demasiados observadores o cambios frecuentes, el manejo del estado puede complicarse, generando notificaciones constantes.
* Bad, because Si un observador modifica el estado del sujeto, puede causar bucles de notificación o sobrecarga en el sistema.
* Bad, because Con muchos observadores, puede ser difícil rastrear qué clase ha provocado un cambio específico.

### Patrón Bus de eventos

El patrón Event Bus usa un intermediario (el bus de eventos) para gestionar la comunicación entre el emisor de un evento y sus suscriptores. Los suscriptores se registran para recibir ciertos tipos de eventos, y el Event Bus los distribuye cuando el emisor los genera.

* Good, because Los emisores y receptores no necesitan conocerse entre sí, solo interactúan con el bus de eventos.
* Good, because Permite manejar múltiples tipos de eventos y facilita el registro y eliminación de suscriptores en tiempo de ejecución.
* Good, because El Event Bus puede configurarse para enviar los avisos de forma asincrónica, mejorando el rendimiento y evitando bloqueos en el sistema.
* Bad, because Rastrear el flujo de eventos es más complicado, especialmente si hay varios suscriptores para cada tipo de evento.
* Bad, because En sistemas pequeños, un Event Bus puede agregar una complejidad innecesaria.
* Bad, because Si se maneja incorrectamente, el Event Bus puede consumir recursos debido a la frecuencia o el volumen de eventos.

### Patrón mediador

En el patrón Mediator, un objeto central (el mediador) facilita la comunicación entre múltiples objetos sin que estos se comuniquen directamente entre sí. En lugar de interactuar directamente, los componentes solo se comunican con el mediador, quien decide qué otras clases deben ser notificadas o con cuáles interactuar.

* Good, because Toda la lógica de comunicación está en un solo lugar, lo que permite un control más detallado sobre las interacciones y facilita los cambios.
* Good, because Los objetos no necesitan conocer la existencia de otros objetos, solo del mediador, lo que simplifica las relaciones entre componentes.
* Good, because Ayuda a reducir la complejidad del sistema cuando las interacciones entre objetos son numerosas o complejas.
* Bad, because Si el mediador gestiona muchas interacciones, puede convertirse en una clase muy grande y complicada de mantener.
* Bad, because Si el mediador centraliza demasiada lógica, puede volverse un cuello de botella o un punto único de fallo.
* Bad, because Aunque los componentes están desacoplados entre sí, dependen del mediador, lo que puede limitar la flexibilidad si el mediador se vuelve complicado o se modifica frecuentemente.

## Links

* RF-11 Gestión de incidencias
