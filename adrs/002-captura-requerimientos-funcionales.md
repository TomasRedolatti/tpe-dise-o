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

Funcionalidades:
Funcionalidades Agregadas desde la Vista del Usuario
1. Gestión de Clientes (Servicio de Clientes)

    Agregar Cliente: Permite a los usuarios registrar nuevos clientes con sus datos personales.
    Editar Cliente: Modificación de información personal, como nombre, dirección y contacto.
    Consultar Cliente: Visualización de los datos registrados de un cliente.
    Eliminar Cliente: Baja lógica de clientes no activos.

2. Gestión de Pedidos (Servicio de Pedidos)

    Crear Pedido: Los usuarios pueden crear un pedido seleccionando productos y asociando al cliente registrado.
    Modificar Pedido: Actualización de productos, cantidades o información relevante del pedido.
    Cancelar Pedido: Posibilidad de cancelar pedidos antes de ser procesados.
    Consultar Estado de Pedido: Permite a los usuarios verificar el estado del pedido (en proceso, despachado, entregado).

3. Optimización de Rutas y Reparto (Servicio de Reparto y Rutas)

    Asignar Pedido a Ruta: Asignación automática de pedidos a rutas de reparto optimizadas.
    Consultar Ruta: Visualización del itinerario asignado a cada pedido.
    Modificar Ruta: Ajustes manuales en la asignación de rutas en casos excepcionales.

4. Gestión de Pagos (Servicio de Pagos)

    Procesar Pago: Integración con MercadoLibre para procesar pagos en línea.
    Consultar Pago: Revisión del estado del pago asociado a un pedido.
    Reembolsar Pago: Emisión de reembolsos en casos de cancelación.

5. Reportes y Estadísticas (Servicio de Estadísticas)

    Generar Reporte de Pedidos: Informe consolidado de pedidos realizados en un periodo determinado.
    Generar Reporte de Repartos: Estadísticas sobre eficiencia y rutas completadas.
    Reporte de Clientes Activos: Listado y estadísticas de clientes recurrentes.

6. Gestión de Incidencias (Servicio de Incidencias)

    Reportar Incidencia: Registro de problemas durante el reparto, como fallos en la entrega o problemas de pago.
    Consultar Incidencias: Revisión y seguimiento de las incidencias registradas
