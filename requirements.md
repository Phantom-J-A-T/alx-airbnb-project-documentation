1. User Authentication
Overview:

This feature enables secure user registration, login, and session management using JWT-based authentication.

API Endpoints:
Method	Endpoint	Description
POST	/api/auth/register	Register a new user
POST	/api/auth/login	Authenticate and return JWT
GET	/api/auth/profile	Get authenticated user profile
POST	/api/auth/logout	Invalidate user session
Input/Output Specifications:
Registration (POST /api/auth/register)

Input (JSON):

{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "password": "SecurePass123",
  "role": "guest"
}


Output (Success):

{
  "message": "User registered successfully",
  "user_id": 101
}

Login (POST /api/auth/login)

Input (JSON):

{
  "email": "john@example.com",
  "password": "SecurePass123"
}


Output (Success):

{
  "token": "jwt-token-string",
  "expires_in": 3600
}

Validation Rules:

Email must be unique and in correct format.

Password must be at least 8 characters with letters, numbers, and symbols.

Role must be one of guest, host, admin.

Performance Criteria:

Registration/Login request ≤ 200ms under normal load.

JWT expiration configurable (default 1 hour).

2. Property Management
Overview:

Allows hosts to create, update, delete, and view property listings.

API Endpoints:
Method	Endpoint	Description
POST	/api/properties	Create a new property
GET	/api/properties	Get list of all properties
GET	/api/properties/{id}	Get property details by ID
PUT	/api/properties/{id}	Update property details
DELETE	/api/properties/{id}	Delete a property by ID
Input/Output Specifications:
Create Property (POST /api/properties)

Input (JSON):

{
  "name": "Beachfront Villa",
  "description": "Beautiful 3-bedroom villa by the beach",
  "price_per_night": 200.00,
  "location_id": 5,
  "host_id": 2
}


Output (Success):

{
  "message": "Property created successfully",
  "property_id": 45
}

Validation Rules:

price_per_night must be numeric and > 0.

name is required, max length 150 characters.

location_id and host_id must exist in DB.

Performance Criteria:

Fetch all properties with pagination.

Property creation ≤ 300ms under normal load.

3. Booking System
Overview:

Handles property booking requests, cancellations, and status tracking.

API Endpoints:
Method	Endpoint	Description
POST	/api/bookings	Create a new booking
GET	/api/bookings	Get list of all bookings
GET	/api/bookings/{id}	Get booking details by ID
PUT	/api/bookings/{id}	Update booking status
DELETE	/api/bookings/{id}	Cancel a booking
Input/Output Specifications:
Create Booking (POST /api/bookings)

Input (JSON):

{
  "user_id": 3,
  "property_id": 45,
  "start_date": "2025-10-10",
  "end_date": "2025-10-15"
}


Output (Success):

{
  "message": "Booking created successfully",
  "booking_id": 12,
  "total_price": 1000.00
}

Validation Rules:

Start date < End date.

Property must be available for requested dates.

Booking total_price = number_of_days × price_per_night.