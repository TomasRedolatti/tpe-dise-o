# Iteración 1: Análisis y Diseño Inicial

## Decisiones de Diseño

- **Arquitectura Monolítica a Microservicios**: Se propone la transición a una arquitectura de microservicios, separando las funcionalidades críticas (Clientes, Pedidos, Reparto y Rutas, y Pagos) en servicios independientes. Esto mejora la escalabilidad y mantenimiento.
- **Comunicación HTTP/REST**: Los microservicios se comunicarán entre sí mediante HTTP/REST, lo que facilita la integración con los clientes (PC y móvil).
- **Bases de Datos**: Se mantiene el uso de bases de datos SQL para los microservicios de Clientes y Pedidos, aunque se evaluará si conviene adaptarlas o cambiarlas a soluciones no SQL según la carga de datos.

## Artefactos de Arquitectura

- **Vista de Componentes y Conectores (C&C)**:
  - El sistema se divide en microservicios: `Clientes`, `Pedidos`, `Reparto y Rutas`, `Estadísticas`, `Incidencias`, `Pagos`.
  - Cada microservicio se conecta mediante protocolos HTTP/REST.
  - Los servicios críticos estarán más distribuídos para mayor resiliencia.

## Cuestiones Abiertas

- **Persistencia**: Aún se está evaluando si utilizar bases de datos SQL para todos los servicios o considerar alternativas NoSQL.
- **Escalabilidad de Pedidos**: Necesitamos decidir si el microservicio de Pedidos requiere más módulos de escalabilidad.

## Enfoque de Arquitectura

- **Microservicios**: Para facilitar la escalabilidad y flexibilidad, se establece la separación de las funcionalidades en microservicios, mejorando el mantenimiento.

