# Decisión arquitectónica

* Status: accepted
* Deciders: ASS
* Date: 2024-10-31

Technical Story: migración de modelo arquitectónico

## Context and Problem Statement

Basado en nuestra necesidad de cambio por la migración hemos de cambiar el tipo de modelo arquitectónico de la aplicación. Esto nos lleva a ponderar las diversas opciones disponibles para que se realize esta tarea correctamente.

## Decision Drivers

* RF-1 Migración a arquitectura basada en microservicios

## Considered Options

* Arquitectura MVC
* Arquitectura Cliente/Servidor
* Arquitectura por capas
* Arquitectura SOA

## Decision Outcome

Chosen option: "Arquitectura Cliente/Servidor", because al tener en cuenta todos los modelos arquitectónicos, el modelo cliente/servidor se adapta a nuestras necesidades más.

### Positive Consequences

* Facilidad de mantenimiento y despliegue
* Separación de responsabilidades
* Seguridad centralizada
* Escalabilidad

### Negative Consequences

* Latencia en la comunicación
* A medida que aumentan los clientes concurrentes, gestionar múltiples solicitudes al mismo tiempo se vuelve complejo
* Un sistema cliente-servidor depende de una conexión de red estable

## Pros and Cons of the Options

### Arquitectura MVC

La arquitectura Modelo-Vista-Controlador (MVC) es un patrón de diseño que divide una aplicación en tres componentes interdependientes(Modelo, vista y controlador). Esta división permite separar la lógica de negocio de la interfaz de usuario, facilitando el mantenimiento y la escalabilidad.

* Good, because facilita la organización y el mantenimiento al separar la lógica de negocio, la interfaz y el flujo de control.
* Good, because las vistas y modelos pueden reutilizarse en diferentes partes de la aplicación o en otros proyectos.
* Good, because al tener componentes separados, es más sencillo realizar pruebas unitarias de cada parte.
* Bad, because puede ser complejo de implementar y entender, especialmente para desarrolladores principiantes o en proyectos pequeños.
* Bad, because para aplicaciones simples, MVC puede añadir una sobrecarga innecesaria en forma de clases y código adicional.
* Bad, because la fuerte interdependencia entre controlador, modelo y vista puede dificultar ciertos cambios, especialmente en proyectos grandes.

### Arquitectura Cliente/Servidor

Es una arquitectura que se basa en la division del trabajo en dos partes(Cliente y Servidor). La parte del cliente se encarga de mandar solicitudes al servidor y de cargar las respuestas así como interactúa con el usuario. Y la parte del servidor gestiona las solicitudes, accede a los datos y envía las respuestas.
Este modelo permite que varias aplicaciones cliente se conecten a un servidor central, facilitando el acceso a los datos y recursos compartidos.

* Good, because almacena y gestiona los datos en un único servidor, facilitando la administración y seguridad.
* Good, because permite añadir más clientes sin cambiar la estructura básica del servidor.
* Good, because las actualizaciones y cambios se realizan en el servidor sin necesidad de alterar los clientes.
* Bad, because si el servidor falla, los clientes pierden el acceso a los servicios y datos.
* Bad, because con muchos clientes simultáneos, el rendimiento puede verse afectado y se pueden generar cuellos de botella.
* Bad, because requiere una infraestructura de red robusta y servidores potentes, lo que puede elevar costos iniciales y de mantenimiento.

### Arquitectura por capas

Es un modelo de arquitectura que estructura el proyecto por capas lógicas, organizadas por jerarquías y cada una con responsabilidades únicas. Cada capa se comunica solo con las adyacentes ofreciendo y consumiendo servicios.

* Good, because permite una buena modularidad de nuestro proyecto, separando problemas de mantenimiento en problemas mas asequibles y aislados.
* Good, because ideal para un proyecto escalable y mantenible, pues su estructura por capas es muy facil de hacer crecer a futuro.
* Good, because la separacion de responsabilidades de las capas hace muy facil organizar el código y que sea más claro.
* Bad, because en proyectos pequeños, puede que aumente la complejidad innecesariamente sobrecargando la creacion de algunas capas.
* Bad, because la cominicacion entre las capas puede generar latencia, afectando al rendimiento en sistemas grandes.
* Bad, because tiene cierta rigidez en la estructura, en ciertos casos un cambio en una capa puede resultar en cambios en las adyacentes.

### Arquitectura SOA

La arquitectura orientada a servicios (SOA) es un enfoque en el que una aplicación se construye mediante servicios independientes que interactúan a través de la red. Cada servicio es autónomo y se centra en una función específica de negocio, permitiendo que diferentes aplicaciones o módulos los reutilicen.

* Good, because los servicios independientes se pueden usar en múltiples aplicaciones, aumentando la eficiencia y reduciendo el desarrollo redundante.
* Good, because permite escalar cada servicio de forma independiente según la demanda, optimizando recursos.
* Good, because facilita la integración de sistemas heterogéneos, permitiendo que servicios de diferentes tecnologías se comuniquen mediante protocolos estándar.
* Bad, because la orquestación y el monitoreo de múltiples servicios pueden ser complicados y demandan una gestión centralizada.
* Bad, because la comunicación constante entre servicios puede generar una sobrecarga en la red y reducir el rendimiento en algunos casos.
* Bad, because los requisitos de infraestructura, seguridad y mantenimiento de SOA pueden ser elevados, especialmente en entornos con servicios altamente especializados.

## Links

* RF-1 Migración a arquitectura basada en microservicios
