# SDE API Round - IRCTC - WorkIndia

## Project Overview

This project simulates a backend railway management system similar to IRCTC, allowing users to check train availability, book seats, and manage train information via admin access. The system ensures accurate real-time bookings, even during concurrent user actions.

## Tech Stack

- **Language:** JavaScript
- **Framework:** Node.js & Express.js
- **Database:** PostgreSQL
- **Testing Tool:** Postman

## Features
**User Registration & Login**: Secure user authentication using JWT.
**Role-Based Access**: Admins can add, update, and manage train data.
**Seat Availability**: Users can check seat availability between any two stations.
**Real-Time Booking**: Users can book available seats, with real-time updates on availability.

## Setup Instructions

1. Clone the Repository:

git clone https://github.com/Alpeshgarg/SDE_API_Round_WorkIndia.git
cd SDE_API_Round_WorkIndia

2. Install Dependencies:

npm install

3. Configure PostgreSQL: Ensure PostgreSQL is running and create the necessary tables.

Users Table:

CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  username VARCHAR(100),
  password VARCHAR(100),
  role VARCHAR(50)
);

Trains Table:


CREATE TABLE trains (
  id SERIAL PRIMARY KEY,
  source VARCHAR(100),
  destination VARCHAR(100),
  total_seats INT,
  available_seats INT
);

Bookings Table:

CREATE TABLE bookings (
  id SERIAL PRIMARY KEY,
  user_id INT REFERENCES users(id),
  train_id INT REFERENCES trains(id),
  seat_number INT
);
Create a .env File: Create a .env file in the root directory and add the following variables:

DB_USER=your_postgres_username
DB_PASSWORD=your_postgres_password
DB_HOST=localhost
DB_PORT=5432
DB_NAME=your_database_name
SECRET_KEY=your_jwt_secret_key
ADMIN_API_KEY=your_admin_api_key
Run the Project: Start the server:


node index.js
The server will run locally at http://localhost:3000.

API Endpoints
User Registration: POST /auth/register
User Login: POST /auth/login
Admin Add Train (API key required): POST /admin/add_train
Get Train Availability: GET /trains
Book a Seat (JWT required): POST /book_seat/:train_id
Get Booking Details (JWT required): GET /booking/:user_id
Notes
Ensure PostgreSQL is running before starting the application.
Admin routes, like adding trains, require an API key.
