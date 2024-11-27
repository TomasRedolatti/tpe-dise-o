Iteración 4: Implementación y Consolidación de la Arquitectura de Microservicios
Estado

Propuesta aceptada y en implementación. Esta etapa marca la culminación de la transición hacia una arquitectura de microservicios completamente operativa, con un enfoque en la estabilidad, seguridad, escalabilidad y optimización del sistema.
Contexto y Problema

Hasta este momento, la migración hacia microservicios ha sido un proceso progresivo, con la separación de módulos críticos como Clientes, Pedidos, Reparto y Rutas, y Pagos. La necesidad de consolidar todos los microservicios bajo un entorno productivo estable y escalable, junto con la integración de prácticas de seguridad y pruebas de resistencia, es crucial para garantizar que la infraestructura pueda manejar un tráfico elevado y permanezca operativa sin fallos durante picos de demanda.
Decisiones Clave en esta Iteración
1. Finalización de la Integración de Microservicios:

    Integración completa de los microservicios: Todos los microservicios involucrados (Clientes, Pedidos, Reparto, Pagos, Incidencias) se integran completamente en el entorno de Kubernetes. Este entorno permitirá que todos los servicios trabajen de forma autónoma pero sincronizada, sin interferir con otros módulos, y se escalen automáticamente cuando sea necesario.
    Implementación del API Gateway (Nginx): Para centralizar las solicitudes externas, se implementa un API Gateway utilizando Nginx, que manejará las peticiones de los clientes hacia los microservicios. Este enfoque optimiza la gestión del tráfico, ofrece balanceo de carga, y facilita la integración de servicios externos mediante una capa de abstracción.

2. Escalabilidad y Optimización de Recursos:

    Escalabilidad automática con Kubernetes: Se ajustan los contenedores de Kubernetes para habilitar el Horizontal Pod Autoscaling (HPA), de modo que los microservicios más críticos, como Pedidos y Reparto, puedan escalar dinámicamente según la demanda, ajustando el número de réplicas de los pods en función de los parámetros de carga como CPU y memoria.
    Optimización de recursos: Además del ajuste automático de réplicas, se configuran límites y solicitudes de recursos para asegurar que cada servicio tenga suficientes recursos para su operación, sin desperdiciar capacidad en momentos de baja demanda.

3. Seguridad y Autenticación:

    OAuth2 y JWT: Para proteger las interacciones entre los microservicios, se implementa un sistema de autenticación y autorización basado en OAuth2 y JWT (JSON Web Tokens). Cada microservicio deberá validar la autenticidad de las peticiones a través de estos tokens, lo que garantiza que solo los servicios autorizados puedan acceder a recursos protegidos.
    Uso de Istio o Kong: Para gestionar las políticas de seguridad, control de tráfico y monitoreo de fallos de comunicación entre microservicios, se implementa un servicio de seguridad como Istio o Kong. Estas herramientas permiten implementar estrategias avanzadas de enrutamiento, políticas de seguridad y asegurar la comunicación entre servicios, además de gestionar las métricas y registros.

4. Pruebas de Carga y Resistencia:

    Simulación de tráfico con Apache JMeter: Se realizan pruebas de carga utilizando Apache JMeter para simular múltiples solicitudes simultáneas, validando cómo el sistema responde bajo condiciones extremas. Esto incluye medir la capacidad de respuesta de los microservicios, el uso de recursos y el comportamiento de escalabilidad.
    Implementación de mecanismos de resistencia: Para asegurar que el sistema pueda manejar fallos sin interrumpir su operación, se implementan circuit breakers y retry mechanisms. Estos mecanismos aseguran que, si un microservicio falla o se vuelve inaccesible, el sistema pueda seguir funcionando correctamente sin interrupciones críticas.

Vistas Generadas en esta Iteración
Vista de Componentes y Conectores (C&C):

    Se genera una representación visual de todos los microservicios y sus interacciones. Esta vista muestra cómo los servicios se comunican entre sí a través de APIs RESTful y el bus de mensajería RabbitMQ, destacando la dependencia de servicios críticos como Pedidos y Reparto y la infraestructura que facilita su comunicación.

Vista de Despliegue:

    La distribución de los microservicios sobre el clúster de Kubernetes se detalla en esta vista. Se muestra cómo los contenedores están agrupados, cómo se asignan recursos de forma dinámica, y cómo el Horizontal Pod Autoscaler (HPA) asegura la escalabilidad automática.

Flujo General de esta Iteración

    Integración de los Microservicios: Todos los microservicios (Clientes, Pedidos, Reparto, Pagos, Incidencias) se integran en el entorno de producción. Esta integración asegura que todos los servicios interactúan de manera fluida bajo un mismo clúster de Kubernetes, con un API Gateway en Nginx que centraliza todas las solicitudes.

    API Gateway (Nginx): Se configura un API Gateway para gestionar las solicitudes desde los clientes hacia los microservicios individuales. Nginx también maneja la seguridad de las conexiones mediante la configuración de certificados SSL/TLS, garantizando que las comunicaciones sean cifradas y seguras.

    Ajuste de la Escalabilidad: Se configura el Horizontal Pod Autoscaler (HPA) para cada microservicio, permitiendo que el número de réplicas de los pods se ajuste dinámicamente en función de la carga de tráfico, mejorando la eficiencia de los recursos y asegurando un rendimiento óptimo en todo momento.

    Seguridad de las Comunicaciones: Se implementa OAuth2 y JWT para asegurar todas las interacciones entre microservicios. Además, se gestionan políticas de seguridad mediante Istio o Kong, que permiten monitorear y controlar el tráfico entre los microservicios.

    Pruebas de Carga: Se realizan pruebas exhaustivas de carga con JMeter, y se implementan circuit breakers y retry mechanisms para garantizar la resiliencia del sistema ante posibles fallos o picos de tráfico.

Consecuencias
Positivas

    Consolidación de la Arquitectura: La migración completa y la integración de todos los microservicios en un entorno de Kubernetes asegura una arquitectura robusta, escalable y fácil de mantener.
    Escalabilidad y Alta Disponibilidad: La capacidad de escalar automáticamente según la demanda garantiza que el sistema pueda soportar altos volúmenes de tráfico sin comprometer el rendimiento.
    Seguridad Mejorada: La implementación de OAuth2, JWT y políticas de seguridad avanzadas mejora la protección de los servicios y las comunicaciones entre ellos, reduciendo los riesgos de accesos no autorizados.
    Resiliencia: La implementación de pruebas de carga y mecanismos de resistencia asegura que el sistema pueda mantener su operatividad incluso bajo condiciones adversas.

Negativas

    Complejidad Operativa: La implementación de múltiples tecnologías (Kubernetes, Nginx, OAuth2, Istio) y la gestión de seguridad avanzada pueden aumentar la complejidad operativa, lo que puede requerir personal adicional para el mantenimiento y monitoreo.
    Tiempo de Configuración: La configuración de escalabilidad automática, seguridad y políticas de resiliencia puede demandar tiempo y recursos significativos, especialmente en las primeras fases de despliegue.

Alternativas Consideradas

    No implementar Kubernetes y seguir con una infraestructura más tradicional:
        Esta alternativa fue rechazada debido a las limitaciones de escalabilidad y flexibilidad que presenta frente a las crecientes demandas de tráfico.

    No utilizar OAuth2 y JWT, y manejar seguridad con autenticación básica:
        Esta opción fue descartada porque la seguridad del sistema sería significativamente más débil, exponiendo los microservicios a potenciales vulnerabilidades.

Aceptación

La decisión fue aceptada por el equipo, considerando que las ventajas de la infraestructura consolidada y las optimizaciones de seguridad, escalabilidad y resiliencia superan los desafíos operativos.
Implicaciones Futuras

    Próxima iteración:
        Evaluar la optimización de los procesos de despliegue continuo y automatización de pruebas para reducir la complejidad operativa.
        Investigar la incorporación de inteligencia artificial en la optimización de rutas y asignación de recursos logísticos para mejorar aún más la eficiencia del sistema de reparto.
