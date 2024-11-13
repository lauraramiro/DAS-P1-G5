# Decisión sobre versión de stripe

* Status: accepted
* Deciders: ASS
* Date: 2024-11-12

Technical Story: Se decide que version de stripe se usará

## Context and Problem Statement

Se necesita una pasarela de pago que ya se nos da hecha y debemos de saber que version de la misma utilizar en nuestro proyecto.

## Decision Drivers

* RF- 10 Acceso a la pasarela de pago

## Considered Options

* Stripe 28.0.1
* Stripe 22.11.0
* Stripe 20.45.0

## Decision Outcome

Chosen option: "Stripe 28.0.1", because se adapta mas a nuestro ambiente y necesidad con las pasarelas de pago.

### Positive Consequences

* La versión 28.0.1 permite utilizar las características más avanzadas de Stripe, como nuevos métodos de pago, mejor autenticación (como 3D Secure 2), y opciones mejoradas para suscripciones y pagos internacionales. Esto es ideal para empresas que buscan una experiencia de pago moderna y completa.
* Al estar alineada con los estándares de seguridad más recientes, esta versión incorpora los últimos parches de seguridad de Stripe.

### Negative Consequences

* Migrar a la versión 28.0.1 puede requerir actualizaciones de código, ya que introduce cambios que no son retrocompatibles.
* Las nuevas funciones y cambios de diseño en la API pueden requerir que el equipo de desarrollo se familiarice con la nueva estructura de la librería y las clases actualizadas, lo cual podría ralentizar el desarrollo inicial.
* Al ser la última versión, puede presentar algunos errores o inconsistencias menores que Stripe solucionará en futuras actualizaciones. 

## Pros and Cons of the Options

### Stripe 28.0.1

La versión 28.0.1 de la librería Stripe para Java es la más reciente y completa, diseñada para aprovechar al máximo las funcionalidades y mejoras actuales de la API de Stripe. Esta versión incluye soporte para los métodos de pago y las integraciones más avanzadas, optimizaciones de rendimiento, y mejoras en la seguridad, como soporte completo para autenticación avanzada y pagos internacionales.

* Good, because Al estar alineada con las actualizaciones recientes de la API, esta versión es ideal para proyectos que necesitan funcionalidades nuevas y soporte completo de la API actual.
* Good, because Incluye las últimas características de Stripe, como nuevos métodos de pago, integraciones avanzadas y mejores opciones de autenticación, como el soporte de autenticación multifactor.
* Good, because Stripe suele optimizar las últimas versiones para cumplir con los estándares de seguridad actuales y corregir errores. Esto hace que la 28.0.1 sea generalmente más segura y estable.
* Bad, because La versión 28.0.1 puede introducir cambios importantes que no son retrocompatibles. Migrar desde una versión antigua puede requerir ajustes en tu código.
* Bad, because Si has trabajado con versiones más antiguas, algunos métodos y clases podrían haber cambiado, lo que requerirá adaptación y un poco de tiempo para acostumbrarse a los nuevos elementos de la API.

### Stripe 22.11.0

La serie 22.x.x de Stripe para Java es una versión estable y ampliamente utilizada en proyectos en producción. Ofrece un buen equilibrio entre estabilidad y funcionalidad, proporcionando soporte para las características principales de Stripe

* Good, because Incluye soporte para la mayoría de las funciones principales de Stripe, como pagos, suscripciones, y soporte básico para autenticación 3D Secure.
* Good, because Debido a su popularidad, encontrarás más ejemplos, documentación y recursos de la comunidad.
* Good, because La serie 22.x.x es ampliamente utilizada y ha demostrado ser una versión confiable, con menos cambios disruptivos. Ideal para proyectos en producción donde la estabilidad es una prioridad.
* Bad, because Faltan algunas funcionalidades introducidas recientemente, como algunos métodos de pago y mejoras en las integraciones de autenticación.
* Bad, because Aunque es estable, esta serie no cuenta con las optimizaciones de rendimiento de las versiones más recientes, lo que puede ser un inconveniente en aplicaciones de gran escala o con altos volúmenes de transacciones.
* Bad, because A medida que Stripe sigue actualizando su API, algunas funcionalidades podrían volverse incompatibles o generar advertencias si se usa una versión antigua.

### Stripe 20.45.0

La serie 20.x.x es una versión más antigua, que se adapta bien a sistemas heredados o que no planean actualizarse frecuentemente.

* Good, because Cumple con los requisitos de las funciones básicas de Stripe, como pagos y suscripciones, para proyectos que no necesitan las últimas innovaciones.
* Good, because Dado que es más simple y menos compleja que las versiones actuales, es ideal para integraciones en sistemas Java antiguos que no requieren actualizaciones frecuentes.
* Bad, because Carece de soporte para muchas características nuevas de Stripe, como algunos métodos de pago avanzados, integraciones con otros sistemas, y mejoras en autenticación.
* Bad, because Las optimizaciones en cuanto a seguridad y rendimiento que se encuentran en versiones más recientes están ausentes en esta serie, lo que podría afectar a sistemas con altos estándares de seguridad.
* Bad, because Con cada nueva versión de Stripe, las versiones más antiguas tienden a recibir menos soporte, por lo que puede ser complicado encontrar soluciones para problemas específicos o errores.

## Links

* RF- 10 Acceso a la pasarela de pago
