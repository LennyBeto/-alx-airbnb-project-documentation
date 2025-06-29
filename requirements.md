# Airbnb Clone – Technical & Functional Requirements
This document details the technical and functional specifications for the Airbnb Clone's core backend features. 
It comprehensively covers API design, expected inputs and outputs, vital validation rules, and key performance considerations.

##  User Authentication
1. Functional Requirements
- Users can register with a name, email, and password.
- Users can log in using email and password.
- Passwords must be securely hashed.
- JWT tokens are used for authentication.

2. API Endpoints
   -  Register a User
POST /api/v1/auth/register

cpp Copy Edit

Request Body (JSON):

{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "password": "StrongPass123!"
}
Validation:

email must be unique and valid.

password must be at least 8 characters.

Response:

201 Created on success.

JWT token returned in response.

🔸 Login
bash
Copy
Edit
POST /api/v1/auth/login
Request Body:

json
Copy
Edit
{
  "email": "john@example.com",
  "password": "StrongPass123!"
}
Response:

200 OK with JWT token.

401 Unauthorized if credentials are invalid.

🏠 2. Property Management
🔧 Functional Requirements
Hosts can create, update, and delete properties.

Guests can search and view property listings.

🔌 API Endpoints
🔸 Create Property
bash
Copy
Edit
POST /api/v1/properties
Request Body:

json
Copy
Edit
{
  "name": "Ocean View Apartment",
  "description": "A cozy apartment with a great view.",
  "location": "Mombasa",
  "pricepernight": 100.00
}
Authentication Required: Host role

Validation:

pricepernight must be a positive number.

name, description, and location are required.

🔸 Search Properties
bash
Copy
Edit
GET /api/v1/properties?location=Mombasa
Query Params:

location (optional)

price_min, price_max (optional)

Response:

List of matching property objects.

📅 3. Booking System
🔧 Functional Requirements
Guests can book available properties.

Hosts cannot book their own listings.

Bookings include total price calculation.

Prevents overlapping bookings.

🔌 API Endpoints
🔸 Create Booking
bash
Copy
Edit
POST /api/v1/bookings
Request Body:

json
Copy
Edit
{
  "property_id": "uuid-of-property",
  "start_date": "2025-07-01",
  "end_date": "2025-07-05"
}
Validation Rules:

start_date must be in the future.

end_date must be after start_date.

No overlapping bookings allowed.

Response:

json
Copy
Edit
{
  "booking_id": "generated-uuid",
  "total_price": 500.00,
  "status": "pending"
}
🔸 Get User Bookings
bash
Copy
Edit
GET /api/v1/bookings/my
Authentication Required: Yes

Response:

List of user’s past and upcoming bookings.

⚙️ General Performance & Security Criteria
All sensitive data (passwords, tokens) must be securely handled.

Indexes should be used on email, property_id, and booking_id for efficient querying.

Rate limiting and input sanitization should be enforced at API level.

Booking logic must ensure atomic transactions to avoid double bookings.

📦 Covered Features
✅ User Authentication

✅ Property Management

✅ Booking System

More specifications (e.g., Payments, Messaging, Reviews) can be added in future versions of this document.
