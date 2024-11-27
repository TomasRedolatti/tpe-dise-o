1. Disponibilidad - Escenario 01 - Alta disponibilidad de microservicios esenciales

Fuente: Los usuarios del sistema que interactúan con los módulos de Clientes, Reparto y Rutas, y Pagos.

Estímulo: Un aumento en el número de usuarios activos simultáneamente, lo que podría generar sobrecarga en los microservicios esenciales.

Artefacto: Los microservicios de Clientes, Reparto y Rutas, y Pagos deben estar disponibles en todo momento para la operación continua.

Ambiente: El sistema está en producción y está siendo utilizado por miles de usuarios simultáneamente durante una campaña promocional.

Respuesta: El sistema debe:

    Garantizar que los microservicios esenciales estén disponibles al menos un 99.95% del tiempo, sin interrupciones significativas.
    Implementar mecanismos de redundancia y balanceo de carga para distribuir el tráfico y evitar puntos de fallo únicos.
    Ofrecer un sistema de monitoreo que detecte rápidamente caídas o fallos de los microservicios y ejecute procesos automáticos de recuperación.

Medidas de respuesta:

    Disponibilidad: Los microservicios esenciales deben mantener una disponibilidad mínima del 99.95% durante 24/7.
    Recuperación ante fallos: En caso de un fallo, el sistema debe recuperarse en menos de 3 minutos sin afectar a los usuarios.
    Tolerancia a caídas: En caso de caída de un servicio, el tráfico debe ser redirigido a un servicio de respaldo o clúster alternativo en menos de 2 segundos.

2. Escalabilidad - Escenario 02 - Ajuste dinámico de capacidad de pedidos

Fuente: La variabilidad en el número de pedidos que los usuarios realizan durante picos de demanda.

Estímulo: Un aumento inesperado en la cantidad de pedidos debido a una campaña de marketing.

Artefacto: El microservicio de gestión de pedidos debe poder escalar automáticamente para satisfacer la demanda adicional.

Ambiente: El sistema opera en un entorno de producción donde los usuarios pueden hacer pedidos en cualquier momento.

Respuesta: El sistema debe:

    Detectar de manera automática un aumento en la carga y ajustar los recursos del microservicio de pedidos.
    Escalar horizontalmente (agregando más instancias) sin interrupciones en el servicio.
    Proporcionar métricas en tiempo real a los administradores para monitorear el estado de la escalabilidad.

Medidas de respuesta:

    Escalabilidad automática: El sistema debe poder escalar automáticamente sin intervención manual en un máximo de 5 segundos.
    Latencia de escalado: Después de detectar un aumento de carga, el tiempo máximo para ajustar los recursos debe ser de 10 segundos.
    Manejo de picos: El sistema debe poder manejar un 300% de la carga normal sin perder rendimiento.

3. Rendimiento - Escenario 03 - Respuesta rápida en consultas de rutas y pedidos

Fuente: Los gestores de rutas que necesitan consultar información en tiempo real sobre las rutas y pedidos.

Estímulo: La necesidad de realizar consultas rápidas para tomar decisiones logísticas importantes.

Artefacto: El microservicio de consulta de rutas y pedidos debe ofrecer respuestas rápidas, incluso bajo alta demanda.

Ambiente: El sistema está en producción, con múltiples usuarios realizando consultas simultáneamente.

Respuesta: El sistema debe:

    Proporcionar resultados de consulta en menos de 1 segundo, incluso cuando la carga de usuarios sea elevada.
    Optimizar las bases de datos y el uso de caché para reducir el tiempo de acceso a la información más solicitada.
    Asegurar que las consultas a la base de datos no bloqueen otros procesos en el sistema.

Medidas de respuesta:

    Tiempo de respuesta: Las consultas deben tener un tiempo de respuesta de menos de 1 segundo en un 95% de los casos.
    Manejo de consultas concurrentes: El sistema debe ser capaz de manejar al menos 1000 consultas simultáneas sin degradar el rendimiento.
    Uso eficiente de caché: Implementar almacenamiento en caché para respuestas frecuentes, reduciendo el tiempo de acceso a los datos.

4. Modularidad - Escenario 04 - Actualización independiente de microservicios

Fuente: El equipo de desarrollo que necesita realizar actualizaciones o mantenimientos sin interrumpir el servicio.

Estímulo: La necesidad de agregar nuevas funcionalidades o corregir errores en uno de los microservicios.

Artefacto: El sistema debe estar compuesto por microservicios modulares que se puedan actualizar independientemente.

Ambiente: El sistema está en producción, con la necesidad de implementar mejoras y correcciones sin afectar a otros servicios.

Respuesta: El sistema debe:

    Permitir actualizaciones de microservicios de forma independiente, sin causar caídas o interrupciones en otros servicios.
    Garantizar que las dependencias entre microservicios estén claramente definidas y gestionadas.
    Proveer un sistema de pruebas automatizadas que verifique la integridad del sistema tras cada actualización.

Medidas de respuesta:

    Actualización independiente: Los microservicios deben poder ser actualizados y desplegados sin afectar a otros servicios.
    Tiempo de inactividad: El tiempo de inactividad durante las actualizaciones no debe exceder los 2 minutos por microservicio.
    Pruebas post-actualización: Implementar pruebas automatizadas para asegurar que no haya problemas tras las actualizaciones.

5. Seguridad - Escenario 05 - Protección de datos sensibles en el sistema de pagos

Fuente: Los usuarios que realizan pagos a través del sistema.

Estímulo: La necesidad de garantizar la seguridad de los datos de pago de los usuarios.

Artefacto: El sistema de pagos debe garantizar la protección de la información confidencial y transacciones.

Ambiente: El sistema está en producción, procesando pagos en tiempo real.

Respuesta: El sistema debe:

    Encriptar los datos de pago (número de tarjeta, dirección de facturación, etc.) durante la transmisión y almacenamiento.
    Utilizar protocolos seguros como TLS y mecanismos de autenticación fuertes, como autenticación multifactor, para las transacciones.
    Monitorear actividades sospechosas o intentos de acceso no autorizado, alertando al equipo de seguridad.

Medidas de respuesta:

    Cifrado de datos: Todos los datos sensibles deben ser cifrados con un estándar de al menos 256 bits durante la transmisión y el almacenamiento.
    Autenticación robusta: Implementar autenticación multifactor para todas las transacciones financieras.
    Monitoreo de seguridad: Detectar intentos de acceso no autorizado en tiempo real y bloquear accesos sospechosos en menos de 1 segundo.

6. Tolerancia a fallos - Escenario 06 - Recuperación ante fallo del microservicio de pagos

Fuente: El microservicio de pagos, que puede fallar debido a errores internos o fallas en servicios externos.

Estímulo: Un error en el servicio de pagos que impide la ejecución de una transacción.

Artefacto: El sistema debe garantizar la recuperación automática ante cualquier fallo de uno de los microservicios críticos.

Ambiente: El sistema está en producción, y los usuarios necesitan realizar pagos continuamente.

Respuesta: El sistema debe:

    Implementar reintentos automáticos en caso de fallo.
    Redirigir las transacciones fallidas a un servicio de respaldo.
    Notificar a los administradores si la recuperación automática falla.

Medidas de respuesta:

    Tiempo de recuperación: El sistema debe recuperarse de un fallo en el microservicio de pagos en un máximo de 2 minutos.
    Reintentos automáticos: El sistema debe realizar hasta 3 reintentos de pago antes de marcarlo como fallido.
    Recuperación de servicio: Si un microservicio crítico cae, debe ser reemplazado por un servicio de respaldo en menos de 1 segundo.

7. Compatibilidad - Escenario 07 - Acceso a microservicios desde dispositivos móviles y PC

Fuente: Los usuarios finales que acceden a la plataforma desde dispositivos móviles o computadoras de escritorio.

Estímulo: La necesidad de asegurar que el sistema sea accesible tanto desde dispositivos móviles como desde PC.

Artefacto: El sistema de microservicios debe ser compatible con HTTP/REST, garantizando la conectividad desde diferentes tipos de dispositivos.

Ambiente: El sistema opera en un entorno de producción donde los usuarios acceden desde dispositivos móviles y computadoras de escritorio.

Respuesta: El sistema debe:

    Asegurar que todos los microservicios sean accesibles a través de protocolos HTTP/REST.
    Implementar una API RESTful compatible con las versiones más comunes de navegadores y sistemas operativos.
    Verificar que la experiencia del usuario sea consistente, tanto en dispositivos móviles como en PC.

Medidas de respuesta:

    Compatibilidad de API: La API debe ser compatible con los navegadores más utilizados y dispositivos móviles.
    Disponibilidad en múltiples plataformas: El 99% de las interacciones deben ser exitosas, tanto desde dispositivos móviles como desde PC.
    Pruebas de compatibilidad: Realizar pruebas de compatibilidad periódicas en una variedad de dispositivos y navegadores.