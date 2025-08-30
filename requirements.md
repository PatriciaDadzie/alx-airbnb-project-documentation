# Requirement Specifications – Airbnb Clone Backend

This document specifies the **technical and functional requirements** for three core backend features of the Airbnb Clone project: **User Authentication, Property Management, and Booking System**.

---

## 1. User Authentication

### Functional Requirements
- Users can register as **Guest** or **Host**.
- Users can log in using **email & password**.
- Support for third-party authentication (OAuth: Google, Facebook).
- Maintain secure sessions using **JWT**.
- Role-based access control:
  - Guest → can search & book properties.
  - Host → can create & manage property listings.
  - Admin → can manage users, listings, bookings, and payments.

### API Endpoints
- `POST /api/v1/auth/register`
  - **Input:** `{ "name": "John Doe", "email": "john@example.com", "password": "securePass123", "role": "guest|host" }`
  - **Output (201 Created):** `{ "message": "User registered successfully", "userId": "uuid", "token": "jwt_token" }`
- `POST /api/v1/auth/login`
  - **Input:** `{ "email": "john@example.com", "password": "securePass123" }`
  - **Output (200 OK):** `{ "message": "Login successful", "token": "jwt_token" }`
- `GET /api/v1/auth/profile` (JWT protected)
  - **Output:** `{ "id": "uuid", "name": "John Doe", "email": "john@example.com", "role": "guest" }`

### Validation Rules
- Email must be unique and valid format.
- Password must be at least 8 characters, contain upper/lowercase and numbers.
- Role must be either `guest` or `host`.

### Performance Criteria
- Authentication response time < 300ms under normal load.
- Token expiry: 24 hours with refresh capability.

---

## 2. Property Management

### Functional Requirements
- Hosts can create, update, and delete property listings.
- Each property must include title, description, location, price, availability, and amenities.
- Guests can search and filter properties by criteria.

### API Endpoints
- `POST /api/v1/properties`
  - **Input:** `{ "title": "Beach House", "description": "Oceanfront property", "location": "Miami", "price": 120, "amenities": ["wifi", "pool"], "availability": ["2025-06-01", "2025-06-10"] }`
  - **Output:** `{ "message": "Property created", "propertyId": "uuid" }`
- `PUT /api/v1/properties/:id`
  - **Input:** `{ "price": 150, "amenities": ["wifi", "pool", "AC"] }`
  - **Output:** `{ "message": "Property updated successfully" }`
- `DELETE /api/v1/properties/:id`
  - **Output:** `{ "message": "Property deleted successfully" }`
- `GET /api/v1/properties?location=Miami&priceMin=100&priceMax=200`
  - **Output:** `[ { "id": "uuid", "title": "Beach House", "price": 120, "location": "Miami" } ]`

### Validation Rules
- Title length: max 100 characters.
- Price: must be > 0.
- Availability dates: must follow `YYYY-MM-DD`.
- Location must not be empty.

### Performance Criteria
- Property searches should return results within < 500ms for up to 10,000 listings.
- Pagination required for large datasets (default 20 per page).

---

## 3. Booking System

### Functional Requirements
- Guests can book properties for available dates.
- Prevent overlapping/double bookings.
- Guests and hosts can cancel bookings (subject to policy).
- Booking statuses: `pending`, `confirmed`, `canceled`, `completed`.

### API Endpoints
- `POST /api/v1/bookings`
  - **Input:** `{ "propertyId": "uuid", "guestId": "uuid", "startDate": "2025-07-01", "endDate": "2025-07-05" }`
  - **Output:** `{ "message": "Booking created", "bookingId": "uuid", "status": "pending" }`
- `PUT /api/v1/bookings/:id/cancel`
  - **Output:** `{ "message": "Booking canceled", "status": "canceled" }`
- `GET /api/v1/bookings/:id`
  - **Output:** `{ "id": "uuid", "propertyId": "uuid", "guestId": "uuid", "status": "confirmed", "startDate": "2025-07-01", "endDate": "2025-07-05" }`

### Validation Rules
- Start date must be before end date.
- Property must exist and be available for requested dates.
- Guests cannot book their own listings.

### Performance Criteria
- Booking creation should process within < 400ms including availability check.
- System must handle at least 1,000 concurrent booking requests without failure.

---

## ✅ Summary
These specifications define the **inputs, outputs, validation, and performance criteria** for the Airbnb Clone backend. They ensure the system is robust, secure, and scalable while meeting user expectations.
