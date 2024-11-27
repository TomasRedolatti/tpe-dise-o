Iteración 2 - Refinamiento y Ajustes del Diseño
Estado

Propuesta aceptada y validada por el equipo.
Contexto y Problema

Tras la revisión de la Iteración 1, se identificaron varias áreas clave que necesitan ajustes para asegurar que el diseño del sistema sea más escalable, robusto y alineado con los requisitos de calidad. Las principales áreas de mejora incluyen:

    Complejidad en la migración a microservicios: Migrar todos los módulos simultáneamente a microservicios generaría una complejidad técnica considerable y podría provocar errores en producción.
    Falta de estrategias para transacciones distribuidas: No se había definido una estrategia adecuada para coordinar las transacciones entre los microservicios de Pedidos y Pagos, lo que podría generar inconsistencias.
    Limitaciones en la comunicación síncrona: El enfoque inicial de comunicación únicamente síncrona con HTTP/REST no es lo suficientemente flexible para manejar cargas altas y transacciones críticas.
    Seguridad centralizada: Aún no se había implementado una solución centralizada de seguridad en el API Gateway, lo que representaba un riesgo de acceso no autorizado a los microservicios.

Estas cuestiones son esenciales para garantizar que el sistema sea lo suficientemente robusto, eficiente y fácil de mantener a medida que crece.
Decisiones

En esta iteración se realizan los siguientes ajustes y decisiones clave:

    División gradual hacia microservicios:
        En lugar de migrar todos los módulos a microservicios de manera simultánea, se comienza con los módulos más críticos. Los servicios de Clientes y Pagos se migrarán a microservicios independientes.
        Los módulos Pedidos e Incidencias permanecerán temporalmente en una arquitectura monolítica para reducir la complejidad inicial y evitar fricciones en la integración.
    Mensajería híbrida:
        Se implementará RabbitMQ para facilitar la comunicación asíncrona entre servicios críticos como Pedidos e Incidencias. Esto permitirá desacoplar los servicios y reducir la carga en momentos de alta concurrencia, mejorando la resiliencia y escalabilidad del sistema.
        Para las interacciones que requieren un proceso síncrono y de bajo impacto, como las consultas simples a la base de datos, se mantendrá el uso de HTTP/REST.
    Transacciones distribuidas:
        Para garantizar la consistencia de los datos en servicios distribuidos, se adoptará el patrón Sagas para gestionar las transacciones entre los microservicios de Pedidos y Pagos. Este patrón permitirá coordinar procesos complejos y largos, gestionando errores y compensando acciones en caso de fallos durante el proceso de pago o pedido.
    API Gateway:
        Se introducirá Keycloak como proveedor centralizado de autenticación y autorización, gestionando la seguridad de manera uniforme para todos los microservicios.
        Además, se configurará el balanceo dinámico utilizando Nginx para distribuir el tráfico de manera eficiente entre los microservicios, asegurando alta disponibilidad y escalabilidad.

Consecuencias
Positivas

    Escalabilidad: La separación de los módulos críticos y la transición gradual hacia microservicios reduce las dependencias rígidas y facilita la adaptación a cambios en la demanda, lo que mejora la capacidad de escalar el sistema de manera flexible.
    Resiliencia: La introducción de mensajería asíncrona mediante RabbitMQ mejora la capacidad del sistema para manejar picos de tráfico y asegurar la continuidad del servicio incluso en situaciones de alta concurrencia.
    Consistencia: El uso del patrón Sagas garantiza que las transacciones distribuidas entre Pedidos y Pagos se gestionen de manera confiable, con mecanismos para manejar fallos y asegurar la integridad de los datos.
    Seguridad: La incorporación de Keycloak para la autenticación centralizada fortalece la seguridad del sistema, reduciendo el riesgo de acceso no autorizado y mejorando la gestión de permisos entre los microservicios.

Negativas

    Complejidad inicial: La implementación de RabbitMQ y la configuración de Sagas pueden aumentar la complejidad técnica en las primeras etapas de desarrollo, ya que requieren una planificación y configuración detalladas.
    Transición parcial: Mantener algunos módulos en una arquitectura monolítica puede generar fricciones al integrar servicios híbridos (monolíticos y microservicios), lo que podría generar problemas de interoperabilidad en el corto plazo.

Alternativas Consideradas

    Migración total a microservicios desde el inicio:
        Esta alternativa fue rechazada debido a la alta complejidad inicial que implicaría migrar todos los módulos simultáneamente. El riesgo de errores en producción y la dificultad para gestionar el sistema en sus primeras fases fueron factores determinantes en esta decisión.

    Uso exclusivo de HTTP/REST:
        Esta opción fue descartada porque no satisface los requisitos de escalabilidad y resiliencia necesarios para manejar los sistemas críticos como Pedidos e Incidencias, que necesitan una mayor capacidad de desacoplamiento y manejo de eventos asíncronos.

Aceptación

La decisión fue aceptada por el equipo, considerando que los beneficios de esta estrategia gradual y la combinación de mensajería asíncrona con comunicación síncrona a través de HTTP/REST superan las limitaciones identificadas.
Implicaciones Futuras

    Próxima iteración:
        Evaluar la migración completa del módulo Pedidos a microservicios, lo que requerirá la implementación de nuevas estrategias de escalabilidad y optimización, especialmente en el área de manejo de inventarios y actualización de pedidos.
        Considerar la implementación de algoritmos de optimización en el microservicio de Reparto y Rutas para mejorar la eficiencia en la asignación de rutas y tiempos de entrega.
    Monitoreo del desempeño de la solución híbrida:
        Durante las próximas etapas de desarrollo, se monitorizará el rendimiento y la estabilidad de la solución híbrida (mensajería asíncrona y HTTP/REST) para garantizar que se mantengan los niveles de rendimiento esperados y para ajustar la configuración en función de la carga real del sistema.
