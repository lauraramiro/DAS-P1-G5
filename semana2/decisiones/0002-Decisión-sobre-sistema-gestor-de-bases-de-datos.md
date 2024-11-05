# Decisión sobre sistema gestor de bases de datos

* Status: accepted
* Deciders: ASS
* Date: 2024-11-05

Technical Story: Elección del tipo de base de datos

## Context and Problem Statement

Debemos de elegir nuestro tipo de sistema gestor de base de datos para albergar todo lo que relaciona a nuestros clientes y sus pedidos. Necesitamos en total dos bases de datos y la eleccion de sus tipos recaerá en nuestros requisitos en particular. Se elige el gestor puesto que en el enunciado ya se especificó que se iba a escoger una de tipo SQL

## Decision Drivers

* RF-2 Acceso a las bases de datos

## Considered Options

* MySQL
* Microsoft SQL Server
* Azure SQL Database

## Decision Outcome

Chosen option: "MySQL", because es el sistema gestor de base de datos que mas nos puede beneficiar con respecto a nuestras necesidades

### Positive Consequences

* MySQL es una excelente opción para quienes buscan un sistema gratuito y flexible
* A diferencia de Microsoft SQL Server y Azure SQL Database, que pueden implicar costos de licencia y suscripción, MySQL permite una implementación más económica, especialmente para proyectos con un presupuesto limitado.
* MySQL tiene una gran comunidad de desarrolladores y usuarios que contribuyen a su desarrollo y mantenimiento. Esto significa que hay una abundante cantidad de documentación, tutoriales y foros disponibles para resolver problemas y aprender. Además, al ser de código abierto, los desarrolladores pueden modificar el software para adaptarlo a sus necesidades específicas, lo que otorga una gran flexibilidad en su uso y personalización.

### Negative Consequences

* Aunque MySQL es un sistema sólido para muchas aplicaciones, puede carecer de algunas características avanzadas que se encuentran en Microsoft SQL Server, como procedimientos almacenados más sofisticados, integración nativa con herramientas de análisis de datos o características avanzadas de informes.
* En comparación con Microsoft SQL Server, MySQL puede enfrentar desafíos de rendimiento en situaciones de alta carga y grandes volúmenes de datos.
* Aunque hay soporte disponible para MySQL, especialmente a través de Oracle (que ahora es su propietario), la calidad y la disponibilidad de soporte técnico comercial pueden no ser tan robustas como las de Microsoft SQL Server, que ofrece diversas opciones de soporte empresarial. Esto puede ser un inconveniente para organizaciones que requieren asistencia continua o que enfrentan problemas críticos en producción.

## Pros and Cons of the Options

### MySQL

Es un sistema de gestión de bases de datos relacional (RDBMS) de código abierto, ampliamente utilizado en aplicaciones web. Utiliza el lenguaje de consulta estructurado (SQL) para la gestión de datos.

* Good, because MySQL es de código abierto, lo que significa que puedes utilizarlo, modificarlo y distribuirlo sin costo alguno. Esto es especialmente atractivo para startups y desarrolladores independientes.
* Good, because Ofrece un rendimiento sólido para aplicaciones pequeñas y puede escalar adecuadamente para manejar grandes volúmenes de datos. Esto lo hace adecuado tanto para aplicaciones web simples como para sistemas más complejos.
* Good, because Al ser uno de los sistemas de gestión de bases de datos más utilizados, cuenta con una comunidad activa que proporciona documentación, foros y soporte, lo que facilita la resolución de problemas.
* Bad, because Aunque MySQL ofrece muchas características útiles, carece de algunas funcionalidades avanzadas que ofrecen otros sistemas, como las transacciones más complejas y el soporte completo para procedimientos almacenados.
* Bad, because En situaciones de alto rendimiento o cuando se gestionan conjuntos de datos extremadamente grandes, MySQL puede enfrentar limitaciones en comparación con otras bases de datos más optimizadas para cargas de trabajo pesadas.
* Bad, because Aunque existe soporte comercial, la calidad del soporte puede variar dependiendo de si se utiliza la versión gratuita o una suscripción de pago, lo que puede ser un inconveniente para empresas que requieren soporte constante.

### Microsoft SQL Server

Microsoft SQL Server es un sistema de gestión de bases de datos relacional desarrollado por Microsoft. Está diseñado principalmente para entornos empresariales y ofrece un conjunto completo de herramientas para el almacenamiento y análisis de datos. SQL Server permite la creación de bases de datos complejas, incluye capacidades de informes y análisis, y se integra bien con otros productos de Microsoft, como .NET y Azure.

* Good, because SQL Server incluye herramientas poderosas como SQL Server Management Studio (SSMS), que facilita la administración y el desarrollo de bases de datos, así como SQL Server Reporting Services (SSRS) para generar informes complejos.
* Good, because Ofrece características de seguridad integradas, como cifrado de datos, autenticación avanzada y auditorías, lo que lo convierte en una opción atractiva para empresas que manejan datos sensibles.
* Good, because Su integración con otros servicios y aplicaciones de Microsoft, como Azure, Power BI y Office, facilita el desarrollo de soluciones completas que abarcan desde la gestión de datos hasta el análisis y la visualización.
* Bad, because Microsoft SQL Server puede ser costoso, especialmente las ediciones empresariales, que requieren licencias que pueden ser prohibitivas para pequeñas empresas o startups. Además, los costos de soporte y mantenimiento pueden sumar.
* Bad, because SQL Server a menudo requiere más recursos de hardware en comparación con otras soluciones, lo que puede incrementar los costos operativos y de infraestructura.
* Bad, because Aunque existen versiones de SQL Server para Linux, su diseño original y la mayoría de las herramientas están optimizados para Windows, lo que puede limitar la flexibilidad en entornos de servidores mixtos o basados en Linux.

### Azure SQL Database

Azure SQL Database es un servicio de base de datos relacional en la nube de Microsoft que se basa en la tecnología de SQL Server. Este servicio está diseñado para proporcionar un entorno de base de datos escalable y de alta disponibilidad sin la necesidad de gestionar la infraestructura subyacente. Azure SQL Database permite a los desarrolladores crear y administrar bases de datos en la nube con capacidades automáticas de copia de seguridad, recuperación ante desastres y escalabilidad.

* Good, because Azure SQL Database permite ajustar los recursos de manera dinámica según las necesidades del negocio, lo que es ideal para aplicaciones que experimentan picos de carga o crecimiento rápido. Puedes empezar con recursos mínimos y escalar a medida que tu aplicación crece.
* Good, because Al ser un servicio administrado, Microsoft se encarga del mantenimiento, actualizaciones y copias de seguridad, lo que reduce la carga de trabajo para los equipos de TI y permite enfocarse en el desarrollo de aplicaciones.
* Good, because Azure SQL Database se integra perfectamente con otros servicios de Azure, facilitando la creación de soluciones en la nube que incluyen análisis de datos, almacenamiento, y machine learning.
* Bad, because Aunque Azure SQL Database permite pagar solo por lo que se usa, los costos pueden aumentar rápidamente si no se gestionan adecuadamente los recursos, especialmente en entornos de alta disponibilidad o con cargas de trabajo intensivas.
* Bad, because Al ser un servicio en la nube, requiere una conexión a Internet constante, lo que puede presentar problemas de latencia y disponibilidad en entornos donde la conectividad no es confiable.
* Bad, because Como servicio administrado, hay menos control sobre la configuración del sistema y la infraestructura en comparación con un sistema autogestionado, lo que puede ser una desventaja para organizaciones que requieren personalización específica

## Links

* RF-2 Acceso a las bases de datos
