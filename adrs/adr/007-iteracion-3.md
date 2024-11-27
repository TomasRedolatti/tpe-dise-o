# Iteración 3 - Avance en la Integración de Microservicios y Gestión de Rutas

## Status
Propuesta aceptada.

## Contexto y Problema
Se requiere avanzar en la migración de los módulos restantes hacia microservicios y abordar la gestión compleja de rutas de reparto, que es un componente crítico para la logística de la empresa.

## Decisión
1. **Migración del módulo 'Pedidos' a microservicio:**
   - El módulo de pedidos, dado su carácter semi-crítico, es migrado a un microservicio independiente para mejorar la escalabilidad y gestión de las fases del pedido.

2. **Desacoplamiento del módulo 'Reparto y Rutas':**
   - Se separa el módulo de reparto en su propio microservicio para poder gestionar algoritmos de optimización específicos de rutas.

3. **Uso de RabbitMQ y REST:**
   - Se mantiene la combinación de comunicaciones asíncronas para los microservicios críticos y REST para la integración de otros módulos.

4. **Despliegue en Kubernetes:**
   - Los microservicios se despliegan en un clúster de Kubernetes, que facilita el escalado automático y la alta disponibilidad.

5. **Implementación de monitorización:**
   - Se integran **Prometheus** y **Grafana** para la supervisión del rendimiento y estado de los microservicios.

## Consecuencias
### Positivas
- **Escalabilidad y Resiliencia**: El sistema es más ágil y fácil de escalar.
- **Desacoplamiento**: Los módulos de **Pedidos** y **Reparto y Rutas** ahora operan de forma independiente, mejorando la flexibilidad del sistema.
- **Optimización en las rutas**: La asignación de camiones y rutas mejora gracias a los algoritmos especializados.

### Negativas
- **Complejidad del despliegue**: Requiere una infraestructura adicional (Kubernetes y Nginx).
- **Overhead de la mensajería**: RabbitMQ introduce una capa extra de complejidad en la comunicación asíncrona.

## Alternativas Consideradas
1. **No usar RabbitMQ y continuar solo con REST:**
   - Rechazada por la falta de escalabilidad y resiliencia para el procesamiento de pedidos e incidencias.

2. **No migrar a microservicios en esta etapa:**
   - Rechazada, ya que la migración gradual facilita la gestión de riesgos.

## Aceptación
La decisión fue aceptada por el equipo, y se avanzará con la implementación de estas decisiones.

## Implicaciones Futuras
- **Próxima iteración:** Evaluar la optimización de la infraestructura en Kubernetes, añadir seguridad a nivel de microservicios y avanzar con el módulo de **Incidencias**.
