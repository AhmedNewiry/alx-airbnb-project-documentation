# AirBnB Clone Backend: Requirement Specifications

This document outlines the technical and functional requirements for three key backend features of the AirBnB Clone system: **User Authentication**, **Property Management**, and **Booking System**. Each feature includes functional requirements, API endpoints, input/output specifications, validation rules, and performance criteria.

## 1. User Authentication

### Functional Requirements
- **F1.1**: Users (guests, hosts, admins) can register with an email, password, and role.
- **F1.2**: Users can log in using email/password or OAuth (Google, Facebook).
- **F1.3**: Users can update their profile (e.g., name, phone, profile photo).
- **F1.4**: The system ensures secure authentication using JWT and role-based access control (RBAC).

### Technical Requirements
#### API Endpoints
- **POST /api/auth/register**: Register a new user.
- **POST /api/auth/login**: Authenticate a user with email/password.
- **POST /api/auth/oauth**: Authenticate via OAuth (Google, Facebook).
- **PUT /api/users/profile**: Update user profile (authenticated).

#### Input/Output Specifications
- **POST /api/auth/register**
  - **Request**:
    ```json
    {
      "email": "string",
      "password": "string",
      "role": "string (guest|host|admin)",
      "name": "string (optional)"
    }
    ```
  - **Response (201 Created)**:
    ```json
    {
      "user": {
        "user_id": "integer",
        "email": "string",
        "role": "string",
        "name": "string"
      },
      "token": "string (JWT)"
    }
    ```
  - **Error (400 Bad Request)**: `{ "error": "Email already exists" }`
- **POST /api/auth/login**
  - **Request**:
    ```json
    {
      "email": "string",
      "password": "string"
    }
    ```
  - **Response (200 OK)**:
    ```json
    {
      "token": "string (JWT)"
    }
    ```
  - **Error (401 Unauthorized)**: `{ "error": "Invalid credentials" }`
- **POST /api/auth/oauth**
  - **Request**:
    ```json
    {
      "provider": "string (google|facebook)",
      "access_token": "string"
    }
    ```
  - **Response (200 OK)**:
    ```json
    {
      "token": "string (JWT)"
    }
    ```
  - **Error (401 Unauthorized)**: `{ "error": "Invalid OAuth token" }`
- **PUT /api/users/profile**
  - **Headers**: `Authorization: Bearer <JWT>`
  - **Request**:
    ```json
    {
      "name": "string (optional)",
      "phone": "string (optional)",
      "photo_url": "string (optional)"
    }
    ```
  - **Response (200 OK)**:
    ```json
    {
      "user_id": "integer",
      "email": "string",
      "name": "string",
      "phone": "string",
      "photo_url": "string"
    }
    ```
  - **Error (401 Unauthorized)**: `{ "error": "Invalid token" }`

#### Validation Rules
- **Email**: Valid format (e.g., `user@example.com`), unique in Users table.
- **Password**: Minimum 8 characters, includes uppercase, lowercase, number, special character.
- **Role**: Must be one of `guest`, `host`, `admin`.
- **OAuth token**: Validated with provider’s API (Google, Facebook).
- **Profile updates**: Phone must match standard formats (e.g., +1234567890); photo_url must be a valid URL.
- **Errors**: Return 400 for invalid inputs, 401 for authentication failures, 409 for duplicate email.

#### Performance Criteria
- **Response Time**: <500ms for login/register under normal load.
- **Scalability**: Handle 10,000 concurrent authentication requests with Redis caching for JWT validation.
- **Reliability**: 99.9% uptime, with secure password hashing (bcrypt) and encrypted JWT (HS256).
- **Security**: HTTPS, rate limiting (100 requests/min per IP), OWASP-compliant input sanitization.

## 2. Property Management

### Functional Requirements
- **F2.1**: Hosts can create property listings with details (title, description, location, price, amenities, availability).
- **F2.2**: Hosts can edit or delete their existing listings.
- **F2.3**: The system ensures only authenticated hosts can manage listings.

### Technical Requirements
#### API Endpoints
- **POST /api/properties**: Create a new property listing (host only).
- **PUT /api/properties/:id**: Update an existing property (host only).
- **DELETE /api/properties/:id**: Delete a property (host only).

#### Input/Output Specifications
- **POST /api/properties**
  - **Headers**: `Authorization: Bearer <JWT>`
  - **Request**:
    ```json
    {
      "title": "string",
      "description": "string",
      "location": "string",
      "price_per_night": "float",
      "amenities": ["string"],
      "availability": [
        {
          "start_date": "string (YYYY-MM-DD)",
          "end_date": "string (YYYY-MM-DD)"
        }
      ]
    }
    ```
  - **Response (201 Created)**:
    ```json
    {
      "property_id": "integer",
      "host_id": "integer",
      "title": "string",
      "description": "string",
      "location": "string",
      "price_per_night": "float",
      "amenities": ["string"],
      "availability": [
        {
          "start_date": "string",
          "end_date": "string"
        }
      ]
    }
    ```
  - **Error (401 Unauthorized)**: `{ "error": "Host authentication required" }`
- **PUT /api/properties/:id**
  - **Headers**: `Authorization: Bearer <JWT>`
  - **Request**: Same as POST, with optional fields.
  - **Response (200 OK)**: Same as POST.
  - **Error (403 Forbidden)**: `{ "error": "Not authorized to edit this property" }`
- **DELETE /api/properties/:id**
  - **Headers**: `Authorization: Bearer <JWT>`
  - **Response (200 OK)**:
    ```json
    { "message": "Property deleted" }
    ```
  - **Error (404 Not Found)**: `{ "error": "Property not found" }`

#### Validation Rules
- **Title**: Non-empty, max 100 characters.
- **Description**: Max 1000 characters.
- **Location**: Valid address string (e.g., “123 Main St, City, Country”).
- **Price_per_night**: Positive float, max 10000.00.
- **Amenities**: Array of predefined strings (e.g., “wifi”, “parking”).
- **Availability**: Valid date ranges, no overlaps, start_date < end_date.
- **Authorization**: JWT must have `host` role; host_id must match property’s host_id for edits/deletes.
- **Errors**: Return 400 for invalid inputs, 401 for missing JWT, 403 for unauthorized access, 404 for non-existent properties.

#### Performance Criteria
- **Response Time**: <300ms for create/update/delete under normal load.
- **Scalability**: Support 5,000 concurrent listing updates with database indexing on Properties table.
- **Reliability**: 99.9% uptime, with ACID compliance for property data.
- **Storage**: Use AWS S3/Cloudinary for property images, with URLs stored in Properties table.

## 3. Booking System

### Functional Requirements
- **F3.1**: Guests can book a property for specific dates, with validation to prevent double bookings.
- **F3.2**: Guests and hosts can cancel bookings per policy.
- **F3.3**: Users can track booking status (pending, confirmed, canceled, completed).

### Technical Requirements
#### API Endpoints
- **POST /api/bookings**: Create a new booking (guest only).
- **PUT /api/bookings/:id/cancel**: Cancel a booking (guest or host).
- **GET /api/bookings**: Retrieve user’s bookings (guest or host).

#### Input/Output Specifications
- **POST /api/bookings**
  - **Headers**: `Authorization: Bearer <JWT>`
  - **Request**:
    ```json
    {
      "property_id": "integer",
      "start_date": "string (YYYY-MM-DD)",
      "end_date": "string (YYYY-MM-DD)",
      "num_guests": "integer"
    }
    ```
  - **Response (201 Created)**:
    ```json
    {
      "booking_id": "integer",
      "user_id": "integer",
      "property_id": "integer",
      "start_date": "string",
      "end_date": "string",
      "num_guests": "integer",
      "status": "string (pending)"
    }
    ```
  - **Error (400 Bad Request)**: `{ "error": "Dates unavailable" }`
- **PUT /api/bookings/:id/cancel**
  - **Headers**: `Authorization: Bearer <JWT>`
  - **Response (200 OK)**:
    ```json
    {
      "booking_id": "integer",
      "status": "canceled"
    }
    ```
  - **Error (403 Forbidden)**: `{ "error": "Not authorized to cancel this booking" }`
- **GET /api/bookings**
  - **Headers**: `Authorization: Bearer <JWT>`
  - **Response (200 OK)**:
    ```json
    [
      {
        "booking_id": "integer",
        "user_id": "integer",
        "property_id": "integer",
        "start_date": "string",
        "end_date": "string",
        "num_guests": "integer",
        "status": "string"
      }
    ]
    ```
  - **Error (401 Unauthorized)**: `{ "error": "Invalid token" }`

#### Validation Rules
- **Property_id**: Must exist in Properties table.
- **Dates**: start_date < end_date, within property’s availability, no overlap with existing bookings in Bookings table.
- **Num_guests**: Positive integer, within property’s capacity.
- **Status**: Must be one of `pending`, `confirmed`, `canceled`, `completed`.
- **Authorization**: JWT required; for cancellation, user must be the booking’s guest or property’s host.
- **Errors**: Return 400 for invalid inputs, 401 for missing JWT, 403 for unauthorized actions, 404 for non-existent bookings.

#### Performance Criteria
- **Response Time**: <400ms for booking creation under normal load.
- **Scalability**: Handle 10,000 concurrent booking requests with database indexing on Bookings (property_id, start_date, end_date).
- **Reliability**: 99.9% uptime, with transactional integrity for booking creation (rollback on payment failure).
- **Concurrency**: Use database locks to prevent double bookings during high load.

## Notes
- **Scope**: This document covers three key features, aligning with the project requirements from `features-and-functionalities/`.
- **Dependencies**: Relies on PostgreSQL/MySQL database, JWT for authentication, and third-party services (AWS S3, Stripe, SendGrid).
- **Future Extensions**: Add requirements for other features (e.g., Payments, Notifications) or detailed acceptance criteria.
- **Repository**: Store in the root directory of `alx-airbnb-project-documentation`.

---