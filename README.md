# Fitness Class Booking API

This project is a simple fitness class booking API built with FastAPI. It allows users to view upcoming classes, book classes, and view their bookings. The data is stored in memory for simplicity, as per the project requirements.

## Features

*   **List Classes:** Get a list of upcoming fitness classes, with the option to view class times in a specified timezone.
*   **Book Class:** Book a slot in an available upcoming class.
*   **View Bookings:** Retrieve all bookings made by a specific email address.
*   **In-Memory Data:** Uses dictionaries for storing class and booking data (suitable for development/demonstration, not production).
*   **Timezone Handling:** Classes are created in IST and can be viewed in other timezones.
*   **Basic Validation:** Includes checks for class existence, past class booking, slot availability, and duplicate bookings by email.

## Technologies Used

*   **FastAPI:** High-performance, easy-to-use web framework.
*   **Uvicorn:** ASGI server to run the FastAPI application.
*   **Pydantic:** Data validation and settings management.
*   **python-jose & passlib:** (Included in original pip command, though not explicitly used in the provided code snippets for auth - good to keep if future auth is planned).
*   **pytz:** For handling timezones.
*   **uuid:** For generating unique booking IDs.

## Setup and Running Locally

These instructions assume you have Python 3.7+ installed.

1.  **Clone the repository:** bash git clone cd

2.  **Create a virtual environment (recommended):** bash python -m venv venv source venv/bin/activate # On Windows use venv\Scripts\activate


3.  **Install dependencies:**

    Create a `requirements.txt` file in the root of your project with the following content:
	fastapi
	uvicorn
	python-multipart
	python-jose[cryptography]
	passlib[bcrypt]
	pytz
	pydantic[email]
	# pyngrok # Only needed if you plan to use ngrok for public access

Then install: bash pip install -r requirements.txt

4.  **Run the application:**

    Save the provided Python code (without the `!pip install` lines and the Colab-specific ngrok/uvicorn running code) into a file, e.g., `main.py`.

    Then run the Uvicorn server: bash uvicorn main:app --reload --port 8000

The `--reload` flag is useful during development as it restarts the server whenever you make code changes. You can omit it for production.
The application will be running at `http://127.0.0.1:8000`.

## API Documentation

Once the server is running, you can access the automatically generated interactive API documentation (Swagger UI) at:

*   `http://127.0.0.1:8000/docs`

Or the alternative ReDoc documentation at:

*   `http://127.0.0.1:8000/redoc`

These docs allow you to explore the available endpoints and test them directly from your browser.

## Endpoints

*   `GET /classes`: Get a list of upcoming classes.
    *   **Query Parameters:** `timezone` (optional, e.g., `UTC`, `America/New_York`). Defaults to `UTC`.
*   `POST /book`: Book a class.
    *   **Request Body:** JSON object with `class_id`, `client_name`, and `client_email`.
*   `GET /bookings`: Get bookings for a specific email.
    *   **Query Parameters:** `client_email` (required).

## Data Storage

The application uses in-memory dictionaries (`classes_db` and `bookings_db`) to store data. This means the data is **not persistent** and will be lost every time the application is stopped and restarted.

For a production application, you would typically integrate with a database (like PostgreSQL, MySQL, MongoDB, SQLite, etc.).

## Timezone Handling

Classes are created using the `Asia/Kolkata` (IST) timezone. The `/classes` endpoint allows clients to request class times converted to a different timezone. Booking times are recorded and returned in UTC.

## Error Handling

The API includes basic error handling for cases like:
*   Invalid timezone requests.
*   Booking a class that doesn't exist.
*   Booking a class that is in the past.
*   Attempting to book a class with no available slots.
*   Attempting to book the same class multiple times with the same email.

## Future Improvements

*   Implement a persistent database (e.g., SQLite, PostgreSQL).
*   Add user authentication and authorization.
*   Enhance input validation.
*   Add unit and integration tests.
*   Implement more sophisticated booking logic (e.g., cancellations, waiting lists).
*   Add pagination and filtering for class and booking lists.
*   Containerize with Docker.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## License
