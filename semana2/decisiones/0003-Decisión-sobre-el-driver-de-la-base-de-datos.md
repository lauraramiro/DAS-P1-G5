# Decisión sobre el driver de la base de datos

* Status: accepted
* Deciders: ASS
* Date: 2024-11-05

Technical Story: Elección sobre el tipo de driver de la base de datos

## Context and Problem Statement

Tras la elección de nuestro sistema gestor de bases de datos, tenemos que elegir que tipo de driver nos conviene más a la hora de manejarnos con MySQL. Esto es necesario para poder operar con nuestras previas elecciones

## Decision Drivers

* RF-2 Acceso a las bases de datos

## Considered Options

* ODBC/Open Database Connectivit
* JDBC/Java Database Connectivity

## Decision Outcome

Chosen option: "JDBC/Java Database Connectivity", because coincide con nuestros objetivos y nos es conveniente por diversos motivos.

### Positive Consequences

* JDBC está optimizado para aplicaciones Java y permite una conexión más directa con MySQL, reduciendo la sobrecarga de la conexión y mejorando el rendimiento en aplicaciones escritas en este lenguaje.
* JDBC permite el acceso a funcionalidades avanzadas y específicas de MySQL, como el manejo de transacciones, el uso de conexiones seguras (SSL/TLS) y tipos de datos específicos de MySQL, lo que enriquece el desarrollo y la funcionalidad de la aplicación.
* A diferencia de ODBC, JDBC no necesita una configuración adicional en el sistema operativo, como la instalación de controladores o DSNs. En Java, simplemente se añade el controlador JDBC de MySQL como dependencia y se configura directamente en el código, facilitando la integración.

### Negative Consequences

* JDBC está limitado al ecosistema Java, lo cual significa que, si el proyecto necesita ser migrado o tener soporte en otros lenguajes o plataformas (como Python, .NET, o herramientas de visualización), será necesario cambiar la estrategia de conexión o usar otro controlador.
* A diferencia de ODBC, que permite la conexión desde diferentes plataformas y lenguajes con una configuración unificada, JDBC solo es compatible con Java. Esto limita la capacidad de interactuar con MySQL desde otras aplicaciones o lenguajes si estos no están en el entorno Java.
* JDBC requiere el controlador específico de MySQL para funcionar, lo que significa que la conexión y el rendimiento dependen de la calidad de este controlador. Si el controlador JDBC de MySQL presenta problemas o tiene limitaciones, puede afectar el rendimiento o la estabilidad de la aplicación.

## Pros and Cons of the Options

### ODBC/Open Database Connectivit

ODBC es un estándar que permite a las aplicaciones acceder a sistemas de gestión de bases de datos (DBMS) mediante una interfaz común. ODBC proporciona una forma de conectar aplicaciones a bases de datos, independientemente del sistema operativo o el DBMS subyacente.

* Good, because ODBC es compatible con múltiples lenguajes de programación y plataformas, lo que lo hace adecuado para aplicaciones que no están limitadas a Java.
* Good, because Permite conectar diversas bases de datos utilizando el mismo conjunto de llamadas a la API, facilitando la migración entre diferentes DBMS.
* Good, because Muchos sistemas y herramientas de terceros, como hojas de cálculo y aplicaciones de informes, utilizan ODBC para acceder a bases de datos.
* Bad, because La capa adicional de abstracción puede introducir cierta sobrecarga en comparación con un controlador específico de la base de datos como JDBC.
* Bad, because La configuración de ODBC puede ser más compleja y requerir más pasos, especialmente en entornos multiplataforma.
* Bad, because Algunas características específicas de MySQL pueden no estar completamente soportadas o pueden requerir ajustes adicionales.

### JDBC/Java Database Connectivity

JDBC es una API de Java que permite a las aplicaciones Java interactuar con bases de datos utilizando SQL. Específicamente diseñado para entornos Java, JDBC proporciona un acceso directo y optimizado a bases de datos.

* Good, because Al estar diseñado específicamente para Java, JDBC ofrece un mejor rendimiento y facilidad de uso en aplicaciones Java.
* Good, because JDBC permite el uso de características específicas de MySQL, como transacciones, conexiones a través de SSL, y soporte para tipos de datos específicos.
* Good, because La API de JDBC es más sencilla y directa para desarrolladores Java, facilitando la escritura de código y la gestión de conexiones.
* Bad, because JDBC es específico para el ecosistema Java, lo que puede ser una desventaja si se desea utilizar otros lenguajes o plataformas.
* Bad, because La calidad y el rendimiento de la conexión pueden variar según la implementación del controlador JDBC específico utilizado.
* Bad, because Para utilizar JDBC, se necesita tener conocimientos de programación en Java, lo que puede ser un obstáculo para algunos desarrolladores.

## Links

* RF-2 Acceso a las bases de datos
