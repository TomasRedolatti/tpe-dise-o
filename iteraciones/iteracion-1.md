Iteración 1: Análisis y Diseño Inicial
Decisiones de Diseño

    Arquitectura Monolítica a Microservicios: La transición hacia una arquitectura de microservicios está justificada por la necesidad de escalabilidad, modularidad y una mayor independencia de los equipos de desarrollo. Se identifica que las funcionalidades críticas del sistema (Clientes, Pedidos, Reparto y Rutas, Pagos, Estadísticas e Incidencias) se beneficiarán enormemente de estar separadas en servicios independientes. Esta separación no solo facilita el mantenimiento, sino que también permite implementar soluciones de alta disponibilidad y recuperación ante fallos, al distribuir las cargas entre múltiples instancias de microservicios.

    Comunicación HTTP/REST: Para asegurar una integración fluida y la interoperabilidad entre microservicios, se establece que la comunicación entre ellos será mediante HTTP/REST. Este enfoque permite que los servicios sean accesibles desde diferentes plataformas, como aplicaciones de escritorio y móviles. Además, facilita la integración con futuros servicios externos, como pasarelas de pago o sistemas de terceros.

    Bases de Datos: Se plantea el uso de bases de datos SQL para los microservicios de Clientes y Pedidos debido a la estructura de datos relacional que requieren. Sin embargo, se considera que algunos servicios, como Reparto y Rutas y Estadísticas, podrían beneficiarse de bases de datos NoSQL, como MongoDB o Cassandra, debido a la naturaleza no estructurada de los datos que manejan (como logs de eventos, rutas dinámicas, y métricas). Esta evaluación se llevará a cabo en fases posteriores del proyecto.

    Seguridad y Autenticación: Se opta por la implementación de un sistema de autenticación centralizado utilizando OAuth2 y JWT para garantizar una autenticación y autorización robusta entre los microservicios, minimizando así posibles brechas de seguridad. Esto permitirá un control de acceso más fino y la integración con sistemas de gestión de identidad externos si fuera necesario.

    Manejo de Configuración: Para asegurar que todos los microservicios utilicen configuraciones consistentes y se adapten dinámicamente a entornos distintos (desarrollo, producción), se adoptará una solución de gestión de configuraciones centralizada como Spring Cloud Config o Consul.

Artefactos de Arquitectura

    Vista de Componentes y Conectores (C&C):
        El sistema se divide en seis microservicios principales: Clientes, Pedidos, Reparto y Rutas, Estadísticas, Incidencias, y Pagos. Cada uno se representa como un componente independiente, que a su vez se conecta a una base de datos específica (SQL o NoSQL según el microservicio) o a un sistema de almacenamiento compartido para la persistencia de datos comunes.
        Los microservicios se comunican mediante HTTP/REST y utilizan JSON como formato estándar para la transferencia de datos.
        Servicios de Orquestación: Un servicio adicional de orquestación estará encargado de coordinar las interacciones entre los microservicios cuando sea necesario. Este servicio puede incluir funcionalidades como la gestión de transacciones distribuidas o el manejo de eventos que disparen procesos en diferentes servicios.

    Escalabilidad y Alta Disponibilidad:
        Se incorporará un sistema de orquestación de contenedores, como Kubernetes, para gestionar la escalabilidad y disponibilidad de los microservicios. Cada microservicio podrá escalar de forma independiente según la carga de trabajo que reciba.
        Los servicios críticos, como Pedidos y Pagos, se desplegarán en múltiples réplicas para garantizar alta disponibilidad.

Cuestiones Abiertas

    Persistencia: Si bien se ha optado por bases de datos SQL para los microservicios de Clientes y Pedidos, aún queda por definir si los servicios que manejan grandes volúmenes de datos no estructurados (como Estadísticas y Reparto y Rutas) deben migrar completamente a soluciones NoSQL. Se plantearán pruebas de rendimiento y escalabilidad para determinar la mejor solución.

    Escalabilidad de Pedidos: El microservicio de Pedidos puede convertirse en un cuello de botella, dado que probablemente maneje una alta cantidad de transacciones simultáneas. Se debe evaluar si es necesario integrar patrones como CQRS (Command Query Responsibility Segregation) o Event Sourcing para mejorar la escalabilidad y la capacidad de respuesta del servicio, separando las operaciones de escritura y lectura.

    Integración con Servicios Externos: Se plantean dudas sobre cómo se gestionará la integración con sistemas externos, como plataformas de pago o servicios de geolocalización para el reparto. Se evaluará el uso de APIs externas y cómo garantizar la compatibilidad con los microservicios del sistema.

Enfoque de Arquitectura

    Microservicios: La elección de microservicios responde al objetivo de modularizar la aplicación, lo que facilita la implementación de nuevas funcionalidades y la evolución del sistema. Cada servicio puede ser desarrollado, probado, y desplegado de manera independiente, lo que reduce los tiempos de desarrollo y mejora la flexibilidad del equipo. Además, al contar con servicios aislados, el mantenimiento de cada uno se puede realizar sin impactar a los otros, permitiendo un ciclo de vida más ágil.

    Despliegue Continuo: La arquitectura soportará un enfoque de integración continua y despliegue continuo (CI/CD), con pipelines automatizados para la construcción, prueba y despliegue de cada microservicio. Esto permitirá actualizaciones frecuentes con mínima interrupción del servicio, asegurando que los cambios puedan ser implementados de manera rápida y segura.

    Monitoreo y Registro Centralizado: Se implementará una solución de monitoreo y logging centralizado, como ELK (Elasticsearch, Logstash, Kibana) o Prometheus + Grafana, para obtener visibilidad completa del estado y rendimiento del sistema. Este enfoque también facilitará la detección temprana de problemas de escalabilidad o fallos en los microservicios.

