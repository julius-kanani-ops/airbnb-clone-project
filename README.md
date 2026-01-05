# airbnb-clone-project
The Airbnb Clone Project is a comprehensive, real-world application designed to simulate the development of a robust booking platform like Airbnb. It involves a deep dive into full-stack development, focusing on backend systems, database design, API development, and application security.
This backend will support various functionalities required to mimic the core features of Airbnb, ensuring a smooth experience for users and hosts.

---
# Project Goals
1. User management - This will implement a secure system for:
- user registration.
- authentication.
- and profile management.

2. Property Management - This service will have features for property listing:
- creation.
- updates.
- retrieval.

3. Booking System - Create a booking mechanism for users to:
- reserve properties.
- manage booking details.

4. Payment processing - This will intergrate a payment system to:
- handle transactions.
- record payment details.

5. Review System - This will allow users to:
- leave reviews.
- provide ratings for properties.

6. Data Optimization - This will ensure efficient:
- data retrieval.
- data storage through database optimizations.

# Tech Stack.
**Django**
: A high-level python web framework used for building the Restful API.

**Django REST Framework**
: Provides tools for creating and managing RESTful APIs.

**PostgreSQL**
: A powerful relational database used for data storage.

**GraphQL**
: Allows for flexible and efficient querying of data.

**Celery**
: For handling asynchronous tasks such as
- sending notifications.
- processing payments.

**Redis**
: Used for caching and session management.

**Docker**
: Containerization tool for:
- consistent development.
- consistent deployment environments.

**CI/CD Pipelines**
: Automated pipelines for testing and deploying code changes.

## Database Design

The application uses a relational database to model core AirBnB domain concepts. The schema is designed to ensure data integrity, scalability, and clear relationships between entities.

### Users
Represents all platform users, including guests and hosts.

**Key Fields**
- `id` (UUID, Primary Key)
- `email` (String, unique)
- `password_hash` (String)
- `role` (Enum: guest, host, admin)
- `created_at` (Timestamp)

**Relationships**
- A user can own multiple properties
- A user can make multiple bookings
- A user can write multiple reviews

---

### Properties
Represents properties listed by hosts.

**Key Fields**
- `id` (UUID, Primary Key)
- `user_id` (Foreign Key → Users.id)
- `title` (String)
- `location` (String)
- `price_per_night` (Decimal)

**Relationships**
- A property belongs to one user (host)
- A property can have multiple bookings
- A property can have multiple reviews

---

### Bookings
Represents reservations made by users for properties.

**Key Fields**
- `id` (UUID, Primary Key)
- `user_id` (Foreign Key → Users.id)
- `property_id` (Foreign Key → Properties.id)
- `start_date` (Date)
- `end_date` (Date)

**Relationships**
- A booking belongs to one user
- A booking belongs to one property
- A booking can have one associated payment

---

### Reviews
Represents user feedback on properties.

**Key Fields**
- `id` (UUID, Primary Key)
- `user_id` (Foreign Key → Users.id)
- `property_id` (Foreign Key → Properties.id)
- `rating` (Integer)
- `comment` (Text)

**Relationships**
- A review belongs to one user
- A review belongs to one property

---

### Payments
Represents payment transactions for bookings.

**Key Fields**
- `id` (UUID, Primary Key)
- `booking_id` (Foreign Key → Bookings.id)
- `amount` (Decimal)
- `payment_method` (String)
- `status` (Enum: pending, completed, failed)

**Relationships**
- A payment belongs to one booking
- Each booking is associated with one payment
