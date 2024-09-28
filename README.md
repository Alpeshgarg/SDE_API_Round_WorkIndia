# SDE API Round - IRCTC - WorkIndia

## Project Overview

This simulates a backend railway management system like the IRCTC wherein users can view train availability, book seats, and manage train information by the admin. It ensures that bookings happen in real-time with accuracy even while the operation is being performed concurrently by different users.

## Tech Stack

- **Language:** JavaScript
- **Framework:** Node.js & Express.js
- **Database:** PostgreSQL
- **Testing Tool:** Postman

## Features
**User Registration & Login**: The user authentication would be secured using JWT.
**Role-Based Access**: Admins can add, update, and manage train data.
**Seat Availability**: Users can check seat availability between any two stations.
**Real-Time Booking**: Users can check seat availability between any two stations.

## Setup Instructions

1. **Clone the Project:**

    ```bash
    git clone https://github.com/Alpeshgarg/SDE_API_Round_WorkIndia.git
    cd SDE_API_Round_WorkIndia
    ```

2. **Install Dependencies:**

    ```bash
    npm install
    ```

3. **Configure PostgreSQL:**

    Ensure PostgreSQL is installed and create the following tables:

    **Users Table:**

    ```sql
    CREATE TABLE users (
      id SERIAL PRIMARY KEY,
      username VARCHAR(100),
      password VARCHAR(100),
      role VARCHAR(50)
    );
    ```

    **Trains Table:**

    ```sql
    CREATE TABLE trains (
      id SERIAL PRIMARY KEY,
      source VARCHAR(100),
      destination VARCHAR(100),
      total_seats INT,
      available_seats INT
    );
    ```

    **Bookings Table:**

    ```sql
    CREATE TABLE bookings (
      id SERIAL PRIMARY KEY,
      user_id INT REFERENCES users(id),
      train_id INT REFERENCES trains(id),
      seat_number INT
    );
    ```

4. **Create a .env File:**

    Create a file called .env in the root of the project directory with the followingvariables:

    ```plaintext
    DB_USER=your_postgres_username
    DB_PASSWORD=your_postgres_password
    DB_HOST=localhost
    DB_PORT=5432
    DB_NAME=your_database_name
    SECRET_KEY=your_jwt_secret_key
    ADMIN_API_KEY=your_admin_api_key
    ```

5. **Run the Project Locally:**

    ```bash
    node index.js
    ```

    The server will run locally at [http://localhost:3000](http://localhost:3000).

6. **Test the API Endpoints:**

    Let's test the following routes using Postman or any equivalent tool

    - **User Registration:** `POST /auth/register`
    - **User Login:** `POST /auth/login`
    - **Admin Add Train (API Key required):** `POST /admin/add_train`
    - **Get Train Availability:** `GET /trains`
    - **Book a Seat (JWT required):** `POST /book_seat/:train_id`
    - **Get Booking Details (JWT required):** `GET /booking/:user_id`

## Important Notes

- The application should run only after PostgreSQL is active.
- Admin routes like the addition of trains need an API key.

