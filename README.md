# Spring Boot Authentication API (JWT + Email Verification + Supabase)

A production-ready **Spring Boot 3** authentication service implementing secure, stateless JWT-based authentication with email verification, Supabase PostgreSQL integration, and Spring Security 6. Designed as a robust foundation for modern backend applications requiring user identity management.

---

## Key Features

### **JWT Authentication**
- Login returns a signed JWT (HS256)
- Stateless authentication using a custom JWT filter
- Automatic token validation on protected routes

### **User Registration & Verification**
- Signup creates new user accounts in Supabase PostgreSQL
- Verification code emailed to the user via SMTP
- Account activation required before login
- Includes "resend verification code" functionality

### **Spring Security 6 Integration**
- Stateless session handling
- Custom authentication provider
- Public access to `/auth/**`
- JWT enforced on all other endpoints

### **Email Delivery (Gmail SMTP)**
- Sends verification codes securely using Gmail App Passwords
- TLS encryption enabled

### **Supabase PostgreSQL**
- Connection pooling supported
- JPA/Hibernate for persistence
- Automatic table creation with `ddl-auto=update`

---

## Architecture Overview

The project is structured for scalability and separation of concerns:

config/           → Security config, JWT filter
controller/       → API endpoints
dto/              → Request payload objects
model/            → JPA entity (User)
repository/       → Database access layer
service/          → Business logic (Auth, JWT, Email)

---

### **Authentication Flow (High-Level)**

1. Client sends credentials to `/auth/login`
2. System validates credentials & account status
3. JWT generated (HS256) with expiration
4. Client includes token in:  
   `Authorization: Bearer <jwt>`
5. `JwtAuthenticationFilter` validates token on every request
6. UserDetails loaded into the SecurityContext

7. ![45A83114-1046-48F8-8980-C76EC7A1CB1A_1_201_a](https://github.com/user-attachments/assets/c8d52f40-9d0e-481a-b8c9-a4673fbc1584)

---

## Technologies Used

| Category     | Technology |
|--------------|------------|
| Framework    | Spring Boot 3.5 |
| Security     | Spring Security 6, JWT |
| Token Library | JJWT (io.jsonwebtoken) |
| Database     | Supabase PostgreSQL |
| ORM          | Hibernate / JPA |
| Email        | Gmail SMTP |
| Build Tool   | Maven |
| Language     | Java 22 |

---

## Endpoints

| Method | Endpoint         | Description                       |
|--------|------------------|-----------------------------------|
| POST   | `/auth/signup`   | Register new user                 |
| POST   | `/auth/verify`   | Verify email with 6-digit code    |
| POST   | `/auth/resend`   | Resend verification code          |
| POST   | `/auth/login`    | Login and receive JWT token       |


---

## Security

- JWT signing using HS256  
- Stateless session management  
- `/auth/**` endpoints public  
- Protected routes enforced by JWT filter  
- Environment-based secrets and DB config  

---

## Database & Email

- Supabase PostgreSQL for user storage  
- Automatic schema creation via JPA  
- Gmail SMTP for verification emails  

---


