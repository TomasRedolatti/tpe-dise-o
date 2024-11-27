# ADR 003: Identificación de Atributos de Calidad

## Disponibilidad
 - Alta disponibilidad para los módulos críticos: Clientes, Reparto y Rutas, y Pagos.

## Escalabilidad
 - Escalar dinámicamente el servicio de Pedidos en función de la carga por hora.

## Performance
 - Respuesta rápida en tiempo real para consultas críticas de rutas y pedidos.

## Modularidad
 - Separar los servicios para facilitar su mantenimiento y evolución.

## Seguridad
 - Proteger la integridad y confidencialidad de los datos en los módulos críticos.

## Tolerancia a fallos
 - Implementar mecanismos re reintento y recuperación en los módulos semi-críticos y críticos.

## Compatibilidad
 - Asegurar que los microservicios sean accesibles mediante protocolos HTTP/REST para clientes PC y móviles.
