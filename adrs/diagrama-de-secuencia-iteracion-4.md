sequenceDiagram
    participant ClientService
    participant OrderService
    participant RouteService
    participant PaymentService
    participant IncidentService
    participant StatisticsService
    participant RabbitMQ
    participant Database

    Note over Client: El cliente envía una solicitud HTTP
    Client->>ClientService: Solicita información de Cliente (getClientData)
    ClientService->>Database: Accede a base de datos de Clientes
    Database-->>ClientService: Retorna datos de Cliente
    ClientService-->>Client: Devuelve datos de Cliente

    Client->>OrderService: Realiza un nuevo pedido (createOrder)
    OrderService->>Database: Guardar pedido en base de datos
    OrderService->>RabbitMQ: Publica evento de pedido nuevo (orderCreated)
    
    Note over RouteService: El microservicio de Rutas optimiza la asignación de rutas
    RouteService->>RabbitMQ: Escucha evento orderCreated
    RouteService->>RouteService: Calcula ruta (using algorithms)
    RouteService->>Database: Guarda ruta calculada
    RouteService-->>OrderService: Retorna ruta optimizada

    Note over PaymentService: Procesa el pago mediante MercadoLibre
    Client->>PaymentService: Solicita transacción de pago (processPayment)
    PaymentService->>PaymentService: Procesa pago con MercadoLibre
    PaymentService-->>Client: Devuelve estado de la transacción

    Client->>IncidentService: Reporta incidente (reportIncident)
    IncidentService->>RabbitMQ: Publica evento incidente (incidentReported)
    IncidentService->>IncidentService: Clasifica y resuelve incidente (using NLP)
    IncidentService-->>Client: Confirma resolución de incidente

    Client->>StatisticsService: Solicita reporte de estadísticas (getStatistics)
    StatisticsService->>Database: Recupera datos históricos
    StatisticsService-->>Client: Devuelve estadísticas

    Note over RabbitMQ: Mensajería asíncrona con RabbitMQ
    RabbitMQ->>RouteService: Envía evento cuando un pedido es creado
    RabbitMQ->>IncidentService: Envía evento cuando se reporta un incidente
