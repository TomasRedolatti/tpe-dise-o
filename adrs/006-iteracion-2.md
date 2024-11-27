# Iteración 2 - Refinamiento y Ajustes del Diseño

## Status
Propuesta aceptada.

## Contexto y Problema
En la iteración 1, se identificaron varias oportunidades de mejora en el diseño inicial, específicamente en:
1. La complejidad de migrar todos los módulos simultáneamente a microservicios.
2. La falta de estrategias específicas para transacciones distribuidas entre **Pedidos** y **Pagos**.
3. Limitaciones en el enfoque inicial de comunicaciones únicamente síncronas.
4. Seguridad centralizada aún no definida en el API Gateway.

Estas cuestiones requieren un ajuste para garantizar un diseño más escalable, robusto y alineado con los atributos de calidad definidos.

## Decisión
En esta iteración se ajustan las siguientes decisiones:
1. **División gradual hacia microservicios:**
   - Migrar primero los módulos críticos **Clientes** y **Pagos** a microservicios independientes.
   - Mantener los módulos **Pedidos** e **Incidencias** en una base monolítica temporal.

2. **Mensajería híbrida:**
   - Implementar **RabbitMQ** para comunicaciones asíncronas entre servicios críticos (ej.: eventos de pedidos e incidencias).
   - HTTP/REST se mantiene para solicitudes sincronizadas de menor impacto.

3. **Transacciones distribuidas:**
   - Usar el patrón **Sagas** para coordinar procesos entre **Pedidos** y **Pagos**.

4. **API Gateway:**
   - Incorporar **Keycloak** como proveedor de autenticación centralizado.
   - Configurar balanceo dinámico mediante **Nginx**.

## Consecuencias
### Positivas
- **Escalabilidad:** La separación inicial de los módulos críticos reduce el impacto de las dependencias rígidas.
- **Resiliencia:** La introducción de mensajería asíncrona reduce la carga en momentos de alta concurrencia.
- **Consistencia:** El patrón Sagas garantiza transacciones distribuidas confiables.
- **Seguridad:** Keycloak centraliza la autenticación y fortalece la seguridad.

### Negativas
- **Complejidad inicial:** La configuración de RabbitMQ y Sagas puede demandar más tiempo.
- **Transición parcial:** Mantener algunos módulos en el monolito puede generar cierta fricción en etapas intermedias.

## Alternativas Consideradas
1. **Migración total a microservicios desde el inicio:**
   - Rechazada por la alta complejidad inicial y riesgo de errores en producción.
2. **Uso exclusivo de HTTP/REST:**
   - Rechazada porque no satisface los requisitos de escalabilidad y resiliencia en sistemas críticos.

## Aceptación
Esta decisión fue aceptada por el equipo, considerando que las ventajas superan las limitaciones identificadas.

## Implicaciones Futuras
- **Próxima iteración:** Evaluar la migración total de **Pedidos** y la implementación de algoritmos de optimización en **Reparto y Rutas**.
- Monitorear el desempeño de la solución híbrida (mensajería y REST).
