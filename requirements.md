# Airbnb Clone Backend: Technical and Functional Requirements

This document outlines the detailed technical and functional specifications for three core backend features: **User Authentication**, **Property Management**, and **Booking System**.

---

## 🔐 1. User Authentication

### Functional Requirements
- Users can register, log in, and log out.
- Authenticated users can access protected endpoints based on their role (guest, host, admin).

### API Endpoints
| Method | Endpoint         | Description              |
|--------|------------------|--------------------------|
| POST   | `/api/register`  | Register a new account   |
| POST   | `/api/login`     | Authenticate user        |
| POST   | `/api/logout`    | Log out and invalidate token |

### Input/Output Specifications
- **Input:** JSON payload with `email`, `password`, `first_name`, `last_name`
- **Output:** Success message with JWT token (for login)

### Validation Rules
- Email must be unique and valid format
- Password must be at least 8 characters
- Names must not be empty

### Performance Criteria
- Login and registration must respond within 2 seconds.
- Passwords must be hashed using a secure algorithm (e.g., bcrypt).

---

## 🏘️ 2. Property Management

### Functional Requirements
- Hosts can create, edit, and delete property listings.
- Users can view available properties with filters.

### API Endpoints
| Method | Endpoint                | Description                |
|--------|-------------------------|----------------------------|
| POST   | `/api/properties`       | Create a new property      |
| GET    | `/api/properties`       | List all properties        |
| GET    | `/api/properties/:id`   | View a specific property   |
| PUT    | `/api/properties/:id`   | Update a property (host only) |
| DELETE | `/api/properties/:id`   | Delete a property (host only) |

### Input/Output Specifications
- **Input:** Property name, description, location, price per night
- **Output:** Property object with unique `property_id`

### Validation Rules
- Name and location must be non-empty
- Price must be a positive decimal
- Only hosts can modify or delete their own listings

### Performance Criteria
- Search/filter should support pagination
- Response time for property listing: ≤ 1.5s

---

## 📆 3. Booking System

### Functional Requirements
- Guests can book available properties for a date range.
- The system calculates total cost and prevents overlapping bookings.

### API Endpoints
| Method | Endpoint             | Description                  |
|--------|----------------------|------------------------------|
| POST   | `/api/bookings`      | Create a new booking         |
| GET    | `/api/bookings`      | View user's bookings         |
| PUT    | `/api/bookings/:id`  | Update a booking (if allowed)|
| DELETE | `/api/bookings/:id`  | Cancel a booking             |

### Input/Output Specifications
- **Input:** Property ID, start date, end date
- **Output:** Booking confirmation with `total_price`, booking ID

### Validation Rules
- Booking dates must not overlap with existing bookings
- Start date must be before end date
- Total price = (number of nights) × (property price per night)

---

## 🔐 Security Considerations
- Use token-based authentication (JWT) for all protected routes
- Role-based access control to restrict host/admin features
- Input validation on all endpoints to prevent SQL injection and data corruption

---

---

## 📝 Summary

These requirements guide backend implementation to ensure robust, secure, and user-centered features for the Airbnb Clone project.
