graph TD
    subgraph API Layer
        APIGateway[API Gateway]
    end

    subgraph Auth Service
        AuthService[Authentication & Authorization Service]
    end

    subgraph Movie Domain
        MovieService[Movie Management Service]
        ShowtimeService[Showtime Service]
        TheatreService[Theatre Service]
    end

    subgraph Booking Domain
        BookingService[Booking Service]
        SeatService[Seat Management Service]
        PaymentService[Payment Gateway Integration]
    end

    subgraph User Domain
        UserService[User Profile Service]
        NotificationService[Notification Service]
    end

    subgraph Infrastructure
        Redis[Redis Cache]
        ServiceBus[Azure Service Bus]
        AzureSQL[(Azure SQL / Cosmos DB)]
        KeyVault[Azure Key Vault]
        BlobStorage[Azure Blob Storage]
    end

    APIGateway --> AuthService
    APIGateway --> MovieService
    APIGateway --> ShowtimeService
    APIGateway --> TheatreService
    APIGateway --> BookingService
    APIGateway --> UserService
    APIGateway --> NotificationService

    BookingService --> SeatService
    BookingService --> PaymentService
    BookingService --> AzureSQL
    BookingService --> ServiceBus
    BookingService --> Redis

    MovieService --> AzureSQL
    ShowtimeService --> AzureSQL
    TheatreService --> AzureSQL

    PaymentService --> ServiceBus
    PaymentService --> AzureSQL

    UserService --> AzureSQL
    NotificationService --> ServiceBus

    AuthService --> AzureSQL
    AuthService --> KeyVault

    AllServices[All Services] -.-> KeyVault
    AllServices -.-> Redis
    AllServices -.-> BlobStorage
