# Cuestionamientos y Alternativas para la Iteración 1

## Contexto y Decisión
En la **Iteración 1**, se tomó la decisión de dividir el sistema monolítico en microservicios según los módulos funcionales definidos: **Clientes**, **Pedidos**, **Reparto y Rutas**, **Estadísticas**, **Incidencias** y **Pagos**. Además, se decidió usar HTTP/REST como protocolo de comunicación, establecer bases de datos independientes (*Database per Service*), y emplear un API Gateway como punto de acceso único para los clientes.

El arquitecto cognitivo realizó un análisis crítico de estas decisiones, planteando cuestionamientos y alternativas para abordar posibles limitaciones o problemas.

---

## Cuestionamiento 1: Complejidad Inicial del Diseño
### Observación
La adopción de microservicios desde el inicio introduce una complejidad significativa, especialmente si el equipo no tiene experiencia previa.

### Preguntas
- ¿El equipo tiene experiencia suficiente para implementar microservicios directamente?
- ¿Es más seguro adoptar un enfoque híbrido temporal para reducir riesgos?

### Alternativa Propuesta
- Desacoplar primero los servicios críticos (**Clientes** y **Pagos**) para evaluar el impacto y realizar una transición gradual.

---

## Cuestionamiento 2: Uso Exclusivo de HTTP/REST
### Observación
HTTP/REST es adecuado para comunicación estándar, pero puede no ser eficiente para módulos con alta concurrencia o procesamiento en tiempo real.

### Preguntas
- ¿Se han considerado alternativas como mensajería asíncrona para reducir latencia?
- ¿Cómo se manejarán picos de carga en módulos críticos?

### Alternativa Propuesta
- Usar mensajería asíncrona (ej., RabbitMQ, Kafka) para módulos críticos como **Pedidos** y **Reparto y Rutas**.
- Mantener HTTP/REST para módulos menos exigentes, como **Estadísticas**.

---

## Cuestionamiento 3: Independencia de Bases de Datos
### Observación
La estrategia *Database per Service* puede generar problemas de consistencia y transacciones distribuidas, especialmente entre servicios interdependientes.

### Preguntas
- ¿Cómo se garantizará la consistencia de los datos entre servicios como **Pedidos** y **Pagos**?
- ¿Qué solución se implementará para gestionar transacciones distribuidas?

### Alternativa Propuesta
- Implementar un patrón de **Sagas** para coordinar transacciones distribuidas.
- Usar una base de datos compartida temporal para servicios interdependientes, con mecanismos de sincronización.

---

## Cuestionamiento 4: Organización del Equipo
### Observación
Dividir el trabajo por microservicio puede generar duplicación de esfuerzos o inconsistencias en las prácticas de desarrollo.

### Preguntas
- ¿Existen estándares definidos para todos los microservicios (ej., logging, autenticación)?
- ¿Cómo se garantizará la colaboración entre equipos con alta interdependencia?

### Alternativa Propuesta
- Crear un equipo centralizado para definir patrones y estándares transversales.
- Implementar herramientas de integración continua y monitoreo para garantizar la consistencia.

---

## Cuestionamiento 5: API Gateway
### Observación
La elección de un API Gateway es adecuada, pero faltan detalles sobre seguridad, balanceo de carga y escalabilidad.

### Preguntas
- ¿Qué estrategia se usará para autenticación y autorización en el API Gateway?
- ¿Cómo se escalará el API Gateway para manejar alta concurrencia?

### Alternativa Propuesta
- Incorporar un sistema de autenticación centralizado en el API Gateway (ej., Keycloak, Auth0).
- Usar un balanceador de carga (ej., Nginx, AWS ELB) para garantizar disponibilidad y escalabilidad.

---

## Conclusión
Las alternativas y cuestionamientos documentados buscan garantizar que el diseño propuesto sea robusto, escalable y alineado con los requisitos del sistema. Este análisis debe ser revisado y discutido antes de proceder con la Iteración 2 del proceso ADD.

