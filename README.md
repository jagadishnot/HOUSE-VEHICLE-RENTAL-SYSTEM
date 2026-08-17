# 🏠🚗🏍️ Rental Marketplace

A full-stack rental marketplace application that connects **property and vehicle owners** with **customers** looking to rent houses, cars, and bikes.

The platform provides role-based authentication, rental listing management, customer booking, booking status management, and a centralized PostgreSQL database.

---

## 📌 Project Overview

**Rental Marketplace** is a web-based rental platform developed using **React.js, Node.js, Express.js, PostgreSQL, and Prisma ORM**.

The system supports two primary user roles:

* **Owner** – Can register, create rental listings for houses, cars, and bikes, manage listings, and view customer bookings.
* **Customer** – Can register, browse available rental listings, view detailed information, and book houses, cars, or bikes.

The application is designed with a clear separation between the owner and customer workflows while maintaining a single secure authentication system.

---

## 🎯 Objectives

The main objectives of this project are:

* Provide a simple platform for renting houses, cars, and bikes.
* Implement secure user registration and login.
* Support separate **Owner** and **Customer** roles.
* Allow owners to publish and manage rental listings.
* Allow customers to browse available listings.
* Provide detailed information about each rental.
* Allow customers to make rental bookings.
* Allow owners to view and manage incoming bookings.
* Store users, listings, and bookings securely in PostgreSQL.
* Provide a responsive and user-friendly interface.

---

# ✨ Key Features

## 🔐 Authentication & Authorization

* User registration
* User login
* Email and password authentication
* Password hashing using bcrypt
* JWT-based authentication
* Role-based authorization
* Owner and Customer dashboards
* Protected routes
* Logout functionality

### Supported Roles

```text
OWNER
CUSTOMER
```

---

# 👤 Owner Features

Owners can use the platform to list their properties and vehicles for rent.

### Owner Dashboard

The owner dashboard provides access to:

* My Listings
* Add Rental
* Manage Listings
* Booking Requests
* Booking History
* Profile
* Logout

### 🏠 Add House

Owners can add house rental information such as:

* House title
* Description
* Rental price
* Location
* Address
* Number of bedrooms
* Number of bathrooms
* Furnishing status
* Parking availability
* House images
* Availability dates

Example:

```text
2BHK Apartment

Location:
Chennai

Bedrooms:
2

Bathrooms:
2

Rent:
₹2,000/day

Parking:
Available
```

---

### 🚗 Add Car

Owners can list cars with details such as:

* Car name
* Brand
* Model
* Manufacturing year
* Rental price
* Location
* Fuel type
* Transmission
* Number of seats
* Description
* Images
* Availability dates

---

### 🏍️ Add Bike

Owners can list bikes with details such as:

* Bike name
* Brand
* Model
* Manufacturing year
* Rental price
* Location
* Engine capacity
* Fuel type
* Description
* Images
* Availability dates

---

# 👥 Customer Features

Customers can browse rental listings and book available properties or vehicles.

### Customer Dashboard

The dashboard provides:

* Houses
* Cars
* Bikes
* Search
* Rental details
* Booking
* My Bookings
* Profile
* Logout

---

## 🏠 Browse Houses

Customers can view available houses.

Each listing displays:

```text
House Image
House Name
Location
Price per Day
Bedrooms
Bathrooms
Availability
```

Customers can click **View Details** to see complete information.

---

## 🚗 Browse Cars

Customers can browse available cars and view:

* Car image
* Brand
* Model
* Year
* Price per day
* Location
* Fuel type
* Transmission
* Seats
* Availability

---

## 🏍️ Browse Bikes

Customers can browse available bikes and view:

* Bike image
* Brand
* Model
* Year
* Price per day
* Location
* Engine capacity
* Fuel type
* Availability

---

# 📅 Booking System

Customers can book an available rental.

### Booking Process

```text
Customer
   ↓
Select Rental
   ↓
View Details
   ↓
Select Start Date
   ↓
Select End Date
   ↓
Calculate Total Price
   ↓
Confirm Booking
   ↓
Booking Created
   ↓
Owner Receives Booking Request
```

---

## 💰 Rental Price Calculation

The system calculates the total rental cost based on the number of rental days.

```text
Total Amount =
Number of Days × Price Per Day
```

Example:

```text
Price per day = ₹2,000

Rental period = 5 days

Total = ₹2,000 × 5
      = ₹10,000
```

---

# 📋 Booking Status

Each booking can have a status.

```text
PENDING
ACCEPTED
REJECTED
COMPLETED
CANCELLED
```

### Booking workflow

```text
Customer creates booking
        ↓
      PENDING
        ↓
   Owner reviews
     /       \
 ACCEPT     REJECT
   ↓           ↓
ACCEPTED    REJECTED
   ↓
COMPLETED
```

---

# 🏢 Owner Booking Management

Owners can see booking requests for their listings.

Example:

```text
Booking ID: #1001

Customer:
Jagadish

Rental:
2BHK Apartment

Start Date:
20/08/2026

End Date:
25/08/2026

Total Amount:
₹10,000

Status:
PENDING
```

The owner can:

```text
[ ACCEPT ]

[ REJECT ]
```

---

# 📊 Customer Booking History

Customers can view their previous and current bookings.

Example:

```text
My Bookings

--------------------------------
2BHK Apartment
Chennai

20 Aug 2026 → 25 Aug 2026

₹10,000

Status: ACCEPTED
--------------------------------
```

---

# 🗄️ Database Design

The application uses **PostgreSQL** as the primary database and **Prisma ORM** for database interaction.

The core database consists of three main entities:

```text
User
Listing
Booking
```

---

## 👤 User Table

Stores both owners and customers.

```text
User
├── id
├── name
├── email
├── password
├── role
└── createdAt
```

Role values:

```text
OWNER
CUSTOMER
```

---

## 🏠 Listing Table

Stores all rental properties and vehicles.

```text
Listing
├── id
├── ownerId
├── type
├── title
├── description
├── price
├── location
├── images
├── status
└── createdAt
```

Listing types:

```text
HOUSE
CAR
BIKE
```

---

## 📅 Booking Table

Stores customer booking information.

```text
Booking
├── id
├── customerId
├── listingId
├── startDate
├── endDate
├── totalAmount
├── status
└── createdAt
```

---

# 🔗 Database Relationships

```text
                 USER
             /           \
         OWNER          CUSTOMER
           |                |
           |                |
           ↓                ↓
       LISTINGS          BOOKINGS
           |                ↑
           └────────────────┘
```

More specifically:

```text
User 1 ──────── * Listing
Owner             Rental Listings


User 1 ──────── * Booking
Customer          Customer Bookings


Listing 1 ────── * Booking
Rental            Rental Bookings
```

---

# 🏗️ System Architecture

```text
                   ┌─────────────────────┐
                   │      React.js       │
                   │      Frontend       │
                   └──────────┬──────────┘
                              │
                         REST API
                              │
                              ↓
                   ┌─────────────────────┐
                   │    Node.js +        │
                   │    Express.js       │
                   │      Backend        │
                   └──────────┬──────────┘
                              │
                         Prisma ORM
                              │
                              ↓
                   ┌─────────────────────┐
                   │     PostgreSQL      │
                   │      Database       │
                   └─────────────────────┘
```

---

# 🛠️ Technology Stack

## Frontend

* React.js
* Vite
* React Router DOM
* JavaScript
* HTML5
* CSS3

## Backend

* Node.js
* Express.js
* REST API
* JWT
* bcryptjs

## Database

* PostgreSQL
* Prisma ORM

## Development Tools

* Visual Studio Code
* Git
* GitHub
* Postman
* pgAdmin

## Planned Services

* Cloudinary – Image storage
* Render – Backend deployment
* Vercel – Frontend deployment

---

# 📁 Project Structure

```text
rental-marketplace/
│
├── client/
│   │
│   ├── public/
│   │
│   ├── src/
│   │   ├── assets/
│   │   │
│   │   ├── components/
│   │   │   ├── Navbar.jsx
│   │   │   ├── ListingCard.jsx
│   │   │   ├── BookingCard.jsx
│   │   │   └── ProtectedRoute.jsx
│   │   │
│   │   ├── pages/
│   │   │   ├── Home.jsx
│   │   │   ├── Login.jsx
│   │   │   ├── Register.jsx
│   │   │   │
│   │   │   ├── owner/
│   │   │   │   ├── OwnerDashboard.jsx
│   │   │   │   ├── AddHouse.jsx
│   │   │   │   ├── AddCar.jsx
│   │   │   │   ├── AddBike.jsx
│   │   │   │   ├── MyListings.jsx
│   │   │   │   └── OwnerBookings.jsx
│   │   │   │
│   │   │   └── customer/
│   │   │       ├── CustomerDashboard.jsx
│   │   │       ├── Houses.jsx
│   │   │       ├── Cars.jsx
│   │   │       ├── Bikes.jsx
│   │   │       ├── ListingDetails.jsx
│   │   │       └── MyBookings.jsx
│   │   │
│   │   ├── context/
│   │   │   └── AuthContext.jsx
│   │   │
│   │   ├── services/
│   │   │   └── api.js
│   │   │
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── index.css
│   │
│   ├── package.json
│   └── vite.config.js
│
├── server/
│   │
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── listingController.js
│   │   └── bookingController.js
│   │
│   ├── middleware/
│   │   ├── authMiddleware.js
│   │   └── roleMiddleware.js
│   │
│   ├── routes/
│   │   ├── authRoutes.js
│   │   ├── listingRoutes.js
│   │   └── bookingRoutes.js
│   │
│   ├── prisma/
│   │   └── schema.prisma
│   │
│   ├── utils/
│   │   └── generateToken.js
│   │
│   ├── .env
│   ├── .gitignore
│   ├── server.js
│   └── package.json
│
├── README.md
└── .gitignore
```

---

# 🔐 Authentication Architecture

The authentication process uses JWT.

```text
REGISTER
   ↓
Validate Input
   ↓
Hash Password
   ↓
Save User
   ↓
Registration Successful
```

Login:

```text
LOGIN
   ↓
Find User
   ↓
Compare Password
   ↓
Generate JWT
   ↓
Return Token
   ↓
React Stores Authentication State
```

Protected request:

```text
React
  ↓
JWT Token
  ↓
Express Middleware
  ↓
Verify Token
  ↓
Check User Role
  ↓
Allow / Reject Request
```

---

# 🔑 Role-Based Authorization

The application prevents users from accessing unauthorized pages.

### Owner

```text
OWNER
 ├── Owner Dashboard
 ├── Add House
 ├── Add Car
 ├── Add Bike
 ├── My Listings
 └── Owner Bookings
```

### Customer

```text
CUSTOMER
 ├── Customer Dashboard
 ├── Browse Houses
 ├── Browse Cars
 ├── Browse Bikes
 ├── Listing Details
 └── My Bookings
```

For example:

```text
Customer → /owner/dashboard
             ↓
           DENIED
```

and:

```text
Owner → /customer/bookings
          ↓
        DENIED
```

---

# 🌐 REST API

## Authentication APIs

### Register

```http
POST /api/auth/register
```

Request:

```json
{
  "name": "Jagadish",
  "email": "jagadish@gmail.com",
  "password": "password123",
  "role": "CUSTOMER"
}
```

---

### Login

```http
POST /api/auth/login
```

Request:

```json
{
  "email": "jagadish@gmail.com",
  "password": "password123"
}
```

---

### Get Current User

```http
GET /api/auth/me
```

Requires:

```text
Authorization: Bearer <JWT_TOKEN>
```

---

# 🏠 Listing APIs

### Create Listing

```http
POST /api/listings
```

Owner authentication required.

---

### Get All Listings

```http
GET /api/listings
```

---

### Get Listing by ID

```http
GET /api/listings/:id
```

---

### Get Owner Listings

```http
GET /api/listings/owner
```

---

### Update Listing

```http
PUT /api/listings/:id
```

---

### Delete Listing

```http
DELETE /api/listings/:id
```

---

# 📅 Booking APIs

### Create Booking

```http
POST /api/bookings
```

---

### Customer Bookings

```http
GET /api/bookings/customer
```

---

### Owner Bookings

```http
GET /api/bookings/owner
```

---

### Update Booking Status

```http
PUT /api/bookings/:id/status
```

Example:

```json
{
  "status": "ACCEPTED"
}
```

---

# ⚙️ Installation

## Prerequisites

Make sure the following are installed:

* Node.js
* npm
* PostgreSQL
* Git
* VS Code
* Postman
* pgAdmin

Check Node.js:

```bash
node -v
```

Check npm:

```bash
npm -v
```

Check PostgreSQL:

```bash
psql --version
```

---

# 🚀 Getting Started

## 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/rental-marketplace.git
```

Move into the project:

```bash
cd rental-marketplace
```

---

# 2. Install Frontend Dependencies

```bash
cd client
npm install
```

---

# 3. Install Backend Dependencies

Open another terminal:

```bash
cd server
npm install
```

---

# 4. Configure PostgreSQL

Create a PostgreSQL database:

```text
rental_marketplace
```

---

# 5. Configure Environment Variables

Create:

```text
server/.env
```

Add:

```env
DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@localhost:5432/rental_marketplace?schema=public"

JWT_SECRET="your_super_secret_jwt_key"

PORT=5000
```

Replace:

```text
YOUR_PASSWORD
```

with your PostgreSQL password.

---

# 6. Run Prisma Migration

From the `server` directory:

```bash
npx prisma migrate dev --name init
```

Then generate Prisma Client:

```bash
npx prisma generate
```

---

# 7. Start Backend

Inside:

```text
server/
```

run:

```bash
npm run dev
```

The backend will run on:

```text
http://localhost:5000
```

---

# 8. Start Frontend

Open another terminal.

Go to:

```bash
cd client
```

Run:

```bash
npm run dev
```

Vite will provide a local development URL, normally:

```text
http://localhost:5173
```

---

# 🔄 Running the Complete Application

You need two terminals.

### Terminal 1 — Backend

```bash
cd server
npm run dev
```

### Terminal 2 — Frontend

```bash
cd client
npm run dev
```

Then open the frontend URL provided by Vite.

---

# 🧪 Testing

The API can be tested using **Postman**.

Recommended testing order:

```text
1. Register Owner
       ↓
2. Login Owner
       ↓
3. Create House
       ↓
4. Create Car
       ↓
5. Create Bike
       ↓
6. Register Customer
       ↓
7. Login Customer
       ↓
8. Browse Listings
       ↓
9. Create Booking
       ↓
10. Login Owner
       ↓
11. View Booking
       ↓
12. Accept / Reject Booking
```

---

# 🛡️ Security

The application implements several security practices:

* Password hashing using bcrypt
* JWT authentication
* Protected API routes
* Role-based authorization
* Environment variables for secrets
* PostgreSQL parameterized queries through Prisma
* Input validation
* CORS configuration
* Sensitive `.env` files excluded from Git

Never commit:

```text
.env
```

to GitHub.

---

# 🖼️ Image Management

The initial version can use image URLs.

The planned production implementation will use:

```text
React
   ↓
Cloudinary
   ↓
Image URL
   ↓
PostgreSQL
```

This prevents large image files from being stored directly in PostgreSQL.

---

# 🔍 Future Enhancements

The project can be expanded with:

### Authentication

* Google OAuth
* Email verification
* Forgot password
* Reset password
* Two-factor authentication

### Rental Features

* Advanced search
* Location-based search
* Price filters
* Category filters
* Availability filters
* Sorting
* Wishlist
* Favorites

### Booking

* Booking cancellation
* Automatic availability checking
* Calendar interface
* Rental extensions
* Booking notifications

### Payments

* Razorpay
* Stripe
* Online payment
* Payment history
* Refund processing

### Communication

* Owner/customer chat
* Booking notifications
* Email notifications
* SMS notifications

### Reviews

```text
Customer
   ↓
Completed Booking
   ↓
Review
   ↓
Rating
```

Example:

```text
★★★★★
4.8 / 5
```

### Advanced Features

* Google Maps integration
* GPS-based location search
* AI-based rental recommendations
* Fraud detection
* Rental price prediction
* Admin dashboard
* Analytics
* Revenue reports

---

# 📱 Responsive Design

The application will be designed to work on:

```text
Desktop
Laptop
Tablet
Mobile
```

The interface will use responsive layouts for:

* Navigation
* Rental cards
* Forms
* Dashboards
* Booking pages
* Listing details

---

# 🚀 Deployment Architecture

The planned production deployment:

```text
                  USERS
                    |
                    ↓
             ┌──────────────┐
             │   Vercel     │
             │    React     │
             └──────┬───────┘
                    |
                 HTTPS
                    |
                    ↓
             ┌──────────────┐
             │   Render     │
             │ Node/Express │
             └──────┬───────┘
                    |
                    ↓
             ┌──────────────┐
             │ PostgreSQL   │
             │   Database   │
             └──────────────┘
```

Images:

```text
React
  ↓
Cloudinary
```

---

# 📊 Project Workflow

```text
                    USER
                     |
              Login / Register
                     |
              ┌──────┴──────┐
              │             │
            OWNER        CUSTOMER
              │             │
              ↓             ↓
       Owner Dashboard   Customer Dashboard
              │             │
       ┌──────┼──────┐      ├──────┬──────┐
       ↓      ↓      ↓      ↓      ↓      ↓
     House   Car    Bike   House   Car    Bike
       │      │      │      │      │      │
       └──────┴──────┘      └──────┴──────┘
              │                    │
              ↓                    ↓
          PostgreSQL           View Listings
                                   |
                                   ↓
                                Booking
                                   |
                                   ↓
                              PostgreSQL
                                   |
                                   ↓
                              Owner View
                                   |
                            Accept / Reject
```

---

# 🧩 Project Modules

| Module              | Description                   |
| ------------------- | ----------------------------- |
| Authentication      | Registration and login        |
| Authorization       | Owner/Customer access control |
| Owner Management    | Manage rental listings        |
| Customer Management | Browse and book rentals       |
| House Rental        | House listing and booking     |
| Car Rental          | Car listing and booking       |
| Bike Rental         | Bike listing and booking      |
| Booking             | Rental booking management     |
| Database            | PostgreSQL data storage       |
| Image Management    | Rental image storage          |
| Dashboard           | Role-specific dashboards      |

---

# 🎓 Academic Project Information

### Project Title

**Rental Marketplace – House, Car & Bike Rental Management System**

### Project Type

Full-Stack Web Application

### Domain

```text
Web Development
Rental Marketplace
Database Management
E-Commerce
```

### Architecture

```text
Client–Server Architecture
```

### Database

```text
PostgreSQL
```

### Frontend

```text
React.js
```

### Backend

```text
Node.js
Express.js
```

### ORM

```text
Prisma
```

### Authentication

```text
JWT + bcrypt
```

---

# 📈 Expected Benefits

The application provides:

* Centralized rental management
* Easy property and vehicle listing
* Simple customer booking
* Secure authentication
* Role-based access
* Digital booking management
* Reduced manual rental management
* Centralized rental information
* Better communication between owners and customers

---

# 🔮 Future Scope

The platform can eventually evolve into a complete rental ecosystem supporting:

```text
Houses
Apartments
Villas
Cars
Bikes
Commercial Vehicles
Equipment
Vacation Rentals
```

Future intelligent features can include:

```text
AI Recommendation System
        ↓
Customer Preferences
        ↓
Previous Bookings
        ↓
Budget
        ↓
Location
        ↓
Recommended Rentals
```

---

# 🤝 Contributing

Contributions are welcome.

### 1. Fork the repository

```bash
git fork
```

### 2. Create a feature branch

```bash
git checkout -b feature/new-feature
```

### 3. Commit changes

```bash
git add .
git commit -m "Add new feature"
```

### 4. Push the branch

```bash
git push origin feature/new-feature
```

### 5. Create a Pull Request

---

# 🐛 Issues

If you find a bug or have a feature request, create an issue in the GitHub repository with:

* Problem description
* Steps to reproduce
* Expected behavior
* Actual behavior
* Screenshots, if applicable

---

# 📄 License

This project is developed for educational and academic purposes.

A suitable open-source license can be added before public production use.

---

# 👨‍💻 Developer

**Jagadish V**

M.Tech Integrated CSE – Data Science & Business Analytics
SRM Institute of Science and Technology

---

# ⭐ Project Summary

**Rental Marketplace** is a full-stack web application designed to simplify the process of renting houses, cars, and bikes.

The platform provides two role-based experiences:

```text
OWNER
↓
Register / Login
↓
Create Rental Listing
↓
Manage Listings
↓
Receive Booking
↓
Accept / Reject Booking
```

and:

```text
CUSTOMER
↓
Register / Login
↓
Browse Rentals
↓
View Details
↓
Select Dates
↓
Book Rental
↓
Track Booking
```

The application combines **React.js, Node.js, Express.js, PostgreSQL, Prisma, JWT, and bcrypt** to provide a secure, scalable, and maintainable rental marketplace architecture.
