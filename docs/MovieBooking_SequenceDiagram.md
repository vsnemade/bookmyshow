sequenceDiagram
    participant User
    participant APIGateway
    participant AuthService
    participant MovieService
    participant ShowtimeService
    participant BookingService
    participant PaymentService
    participant NotificationService

    User->>APIGateway: Login Request
    APIGateway->>AuthService: Authenticate User
    AuthService-->>APIGateway: JWT Token
    APIGateway-->>User: JWT Token

    User->>APIGateway: Search Movies & Showtimes
    APIGateway->>MovieService: Get Movies
    MovieService-->>APIGateway: Movies List
    APIGateway-->>User: Display Movies

    User->>APIGateway: Select Theatre, Time, Seats
    APIGateway->>ShowtimeService: Get Available Showtimes
    ShowtimeService-->>APIGateway: Showtimes
    APIGateway-->>User: Display Showtimes

    User->>APIGateway: Confirm Seat Selection
    APIGateway->>BookingService: Lock Seats
    BookingService-->>APIGateway: Seats Locked

    User->>APIGateway: Make Payment
    APIGateway->>PaymentService: Process Payment
    PaymentService-->>APIGateway: Payment Success
    APIGateway->>BookingService: Confirm Booking
    BookingService-->>APIGateway: Booking Confirmed

    APIGateway->>NotificationService: Send Confirmation
    NotificationService-->>User: Booking Confirmation Notification
