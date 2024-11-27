# ADR 002: Captura de requerimientos funcionales

## Gestión de Clientes
 - Permitir la consulta de datos personales de los clientes.
 - Proveer acceso seguro a los datos sensibles de los clientes (e.g. información personal y pagos)

## Gestión de Pedidos
 - Permitir a los clientes realizar pedidos.
 - Limitar a 3 intentos por cliente en caso de error al realizar un pedido.
 - Garantizar el procesamiento secuencial de las etapas del pedido: preprocesado, autorización y aceptación.

## Gestión de Reparto y Rutas
 - Permitir a los clientes realizar pedidos.
 - Seleccionar dinámicamente entre los dos algoritmos de optimización de rutas.

## Gestión de Estadísticas
 - Proveer informacion sobre el estado de los pedidos y la situación en tiempo real de los camiones.
 - Generar estadísticas sobre los datos históricos de clientes y pedidos.

## Gestión de Incidencias
 - Notificar cualquier problema relacionado con el reparto, como averías de camiones o entregas fallidas.

## Pagos
 - Integrar con la pasarela de pago de MercadoLibre para procesar transacciones seguras.
