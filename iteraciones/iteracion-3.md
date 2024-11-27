Iteración 3 - Avance en la Integración de Microservicios y Gestión de Rutas
Estado

Propuesta aceptada y en proceso de implementación.
Contexto y Problema

El avance de la migración hacia microservicios ha sido exitoso en las etapas anteriores, pero aún queda trabajo por hacer. Es necesario completar la migración de los módulos restantes hacia microservicios para alcanzar la arquitectura distribuida completa. Además, la gestión de rutas de reparto es un componente clave para la eficiencia logística y debe ser abordado con mayor énfasis para optimizar la asignación de recursos y mejorar los tiempos de entrega, que son fundamentales para la operación de la empresa.
Decisiones

En esta iteración, se toman las siguientes decisiones clave:

    Migración del módulo 'Pedidos' a microservicio:
        Se decide migrar el módulo de Pedidos a un microservicio independiente. Dado que Pedidos es considerado semi-crítico en comparación con otros módulos como Pagos, esta migración mejorará la escalabilidad, permitiendo una mejor gestión de las fases del pedido, desde la toma hasta el envío. Esto facilitará la implementación de nuevas funcionalidades de forma aislada, sin afectar a otros módulos.

    Desacoplamiento del módulo 'Reparto y Rutas':
        El módulo de Reparto y Rutas se separa en su propio microservicio. Este módulo se considera clave para la optimización logística, ya que la asignación de camiones y rutas debe ser dinámica y eficiente. Al desacoplar este módulo, se podrán implementar algoritmos de optimización más avanzados (como optimización de rutas, asignación de recursos en tiempo real, y análisis predictivo) sin la interferencia de otros módulos. Además, el desacoplamiento permitirá adaptar los algoritmos de rutas según las necesidades específicas del negocio, mejorando la eficiencia y reduciendo los costos operativos.

    Uso de RabbitMQ y REST:
        Se mantiene la combinación de RabbitMQ para la comunicación asíncrona entre los microservicios críticos (como Pedidos, Reparto y Rutas, e Incidencias), y HTTP/REST para la integración de otros módulos menos críticos o para procesos de consulta de bajo impacto. RabbitMQ sigue siendo fundamental para desacoplar las comunicaciones y mejorar la resiliencia del sistema, especialmente durante picos de alta demanda, evitando que los microservicios dependan de una comunicación síncrona constante que podría generar cuellos de botella.

    Despliegue en Kubernetes:
        Los microservicios se desplegarán en un clúster de Kubernetes, que facilitará el escalado automático y la alta disponibilidad. Kubernetes gestionará la infraestructura, asegurando que los microservicios puedan escalar horizontalmente en función de la demanda. Además, Kubernetes ayudará a manejar el ciclo de vida de los contenedores, simplificando el proceso de despliegue, actualización y recuperación ante fallos.

    Implementación de monitorización:
        Se integran Prometheus y Grafana para la monitorización y visualización del rendimiento de los microservicios. Prometheus se encargará de recolectar métricas y datos de rendimiento de los microservicios, mientras que Grafana ofrecerá una interfaz visual para analizar el estado y comportamiento del sistema en tiempo real. Esto proporcionará visibilidad completa sobre la carga, la disponibilidad y los posibles cuellos de botella, facilitando la toma de decisiones informadas.

Consecuencias
Positivas

    Escalabilidad y Resiliencia: La migración de Pedidos a microservicios, junto con el despliegue en Kubernetes, mejora la capacidad de escalar el sistema de forma flexible y dinámica. Esto permite ajustar rápidamente la infraestructura para satisfacer la demanda creciente y garantizar la continuidad del servicio incluso en momentos de alta carga.
    Desacoplamiento de módulos: Al separar los módulos Pedidos y Reparto y Rutas, se mejora la flexibilidad del sistema. Cada microservicio opera de forma independiente, lo que facilita el desarrollo y mantenimiento de los mismos. Además, permite realizar cambios en un servicio sin impactar en el resto del sistema.
    Optimización en las rutas: La separación del módulo Reparto y Rutas y su integración con algoritmos de optimización permite una asignación más eficiente de los recursos de reparto. Esto puede reducir los tiempos de entrega, mejorar la satisfacción del cliente y disminuir los costos operativos.
    Monitorización avanzada: Con Prometheus y Grafana, se tiene un control más detallado sobre el rendimiento del sistema. Esto facilita la detección de problemas antes de que se conviertan en fallos críticos y permite optimizar continuamente el rendimiento.

Negativas

    Complejidad del despliegue: El uso de Kubernetes y Nginx agrega una capa adicional de complejidad en el despliegue y mantenimiento de la infraestructura. La configuración de estos componentes y la gestión de la red de contenedores pueden requerir recursos adicionales para asegurar que todo funcione sin problemas.
    Overhead de la mensajería: RabbitMQ introduce una capa extra de complejidad en la gestión de la comunicación entre microservicios. La configuración, el monitoreo y la depuración de esta infraestructura asíncrona pueden requerir tiempo y esfuerzo adicional, especialmente en etapas de prueba y despliegue iniciales.

Alternativas Consideradas

    No usar RabbitMQ y continuar solo con REST:
        Esta alternativa fue rechazada debido a que REST no es lo suficientemente escalable ni resiliente para manejar grandes volúmenes de pedidos e incidencias. RabbitMQ es necesario para garantizar que los microservicios puedan procesar eventos de forma asincrónica y sin bloqueo, especialmente en situaciones de alta concurrencia.

    No migrar a microservicios en esta etapa:
        Esta opción fue descartada porque la migración gradual a microservicios ya ha mostrado ser efectiva en etapas anteriores. Mantener una arquitectura monolítica en esta fase no solo limita la escalabilidad y flexibilidad del sistema, sino que también impide la implementación de nuevas funcionalidades de forma modular.

Aceptación

La decisión fue aceptada por el equipo, que considera que los beneficios de avanzar con la migración de los módulos restantes hacia microservicios y mejorar la gestión de rutas superan las complejidades iniciales.
Implicaciones Futuras

    Próxima iteración:
        Evaluar la optimización de la infraestructura en Kubernetes, específicamente para asegurar que los microservicios escalen de forma eficiente en función de la demanda.
        Agregar medidas de seguridad adicionales en el nivel de microservicios, como políticas de acceso específicas, autenticación mutua entre servicios y cifrado de comunicaciones.
        Avanzar con la migración del módulo de Incidencias a microservicio y explorar soluciones para gestionar incidencias de forma más eficiente en el sistema distribuido.


