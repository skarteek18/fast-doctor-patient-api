FastAPI Doctor–Patient Management System

Project Overview

The Doctor–Patient Management System is a RESTful backend application developed using Python and FastAPI.

This project demonstrates API development, database integration, authentication, data validation, CRUD operations, relationships, pagination, filtering and modular backend architecture.

The application allows authenticated users to manage doctor and patient records, assign patients to doctors and securely perform database operations.

Technologies Used

- Python 3.9+
- FastAPI
- Pydantic
- SQLAlchemy ORM
- SQLite
- JWT Authentication
- Uvicorn
- Pytest
- Docker
- Alembic (optional)

Project Features

Level 2: Relationship and Business Logic

Implemented a one-to-many relationship between doctors and patients.

Features:

- Each patient is assigned to one doctor using "doctor_id".
- One doctor can manage multiple patients.
- Patients cannot be assigned to nonexistent doctors.
- Patients cannot be assigned to inactive doctors.
- Retrieve all patients assigned to a specific doctor.

API Endpoint:

"GET /api/v1/doctors/{doctor_id}/patients"

Error Handling:

- "404 Not Found": Doctor does not exist.
- "400 Bad Request": Doctor is inactive.

Level 3: Complete CRUD and Soft Delete

Added complete CRUD operations for managing doctors and patients.

Doctor Endpoints

Method| Endpoint| Description
POST| /api/v1/doctors| Create doctor
GET| /api/v1/doctors| Retrieve doctors
GET| /api/v1/doctors/{id}| Retrieve doctor by ID
PUT| /api/v1/doctors/{id}| Update doctor
PATCH| /api/v1/doctors/{id}| Partially update doctor
DELETE| /api/v1/doctors/{id}| Soft delete doctor

Doctor records are not permanently deleted. Instead, their "is_active" field is set to "False".

Patient Endpoints

Method| Endpoint| Description
POST| /api/v1/patients| Create patient
GET| /api/v1/patients| Retrieve patients
GET| /api/v1/patients/{id}| Retrieve patient by ID
PUT| /api/v1/patients/{id}| Update patient
PATCH| /api/v1/patients/{id}| Partially update patient
DELETE| /api/v1/patients/{id}| Delete patient

Level 4: Advanced Validation

Implemented validation using Pydantic.

Email Validation

- Every doctor must have a unique email address.
- Duplicate email attempts return HTTP 400.

Phone Number Validation

- Phone numbers must contain exactly 10 digits.
- Only numeric characters are accepted.
- Validation uses the regular expression "^[0-9]{10}$".

Example valid phone number: "9876543210"

Level 5: Filtering and Query Parameters

Implemented dynamic filtering to retrieve specific records.

Available Filters

- Filter doctors by specialization.
- Filter doctors by active status.
- Filter patients by age.

Example Requests

GET /api/v1/doctors?specialization=cardiology

GET /api/v1/doctors?is_active=true

GET /api/v1/patients?age_gt=30

Level 6: Pagination

Implemented pagination for efficient retrieval of large datasets.

Pagination Parameters

- "page": Current page number.
- "limit": Number of records per page.

Example Request

GET /api/v1/doctors?page=1&limit=10

Example Response

{
  "total": 25,
  "page": 1,
  "limit": 10,
  "data": []
}

The "data" field contains the records for the requested page.

Level 7: Modular Project Architecture

Organized the application into separate modules for improved maintainability and scalability.

Project Structure

fastapi-doctor-patient-api/
│
├── app/
│   ├── __init__.py
│   ├── main.py
│   ├── database.py
│   ├── models.py
│   ├── schemas.py
│   ├── services.py
│   ├── auth.py
│   │
│   └── routes/
│       ├── __init__.py
│       ├── doctors.py
│       ├── patients.py
│       └── auth.py
│
├── tests/
│   ├── test_doctors.py
│   ├── test_patients.py
│   └── test_auth.py
│
├── .env.example
├── .gitignore
├── requirements.txt
├── Dockerfile
├── alembic.ini
└── README.md

Module Responsibilities

- "main.py": FastAPI application initialization.
- "database.py": Database configuration and session management.
- "models.py": SQLAlchemy database models.
- "schemas.py": Pydantic validation schemas.
- "services.py": Business logic and database operations.
- "auth.py": JWT authentication functionality.
- "routes/": API endpoint definitions.

Level 8: Database Integration

Integrated SQLite with SQLAlchemy ORM to replace in-memory storage.

Database Features

- Persistent storage of doctors and patients.
- SQLAlchemy model relationships.
- Foreign key relationships.
- Database session management.
- Efficient database queries.

Optional enhancement: Alembic database migrations.

Level 9: JWT Authentication

Implemented JWT-based authentication to protect sensitive API operations.

Authentication Endpoint

"POST /api/v1/auth/login"

Security Features

- User authentication.
- JWT access-token generation.
- Password hashing.
- Token validation.
- Protected create, update and delete endpoints.

Authenticated users must provide their access token to access protected endpoints.

Authorization Header

Authorization: Bearer <access_token>

Level 10: Production-Level Improvements

Added additional features to improve security, maintainability and deployment.

Logging

Implemented application logging to track API requests, operations and errors.

CORS Configuration

Configured Cross-Origin Resource Sharing to allow requests from approved origins.

Environment Variables

Used environment variables to manage configuration and sensitive information.

Example ".env.example":

DATABASE_URL=sqlite:///./doctors.db
SECRET_KEY=replace-with-a-secure-secret
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
ALLOWED_ORIGINS=http://localhost:3000

Never commit the actual ".env" file or production secrets.

Docker

Added a Dockerfile to containerize the FastAPI application.

Unit Testing

Used pytest to test API functionality, including:

- Doctor creation and retrieval.
- Patient creation and assignment.
- CRUD operations.
- Duplicate email validation.
- Invalid phone numbers.
- Filtering and pagination.
- JWT authentication.
- Error handling.

API Versioning

Implemented API versioning using the "/api/v1/" prefix.

---

Installation and Setup

1. Clone the Repository

git clone https://github.com/YOUR_USERNAME/fastapi-doctor-patient-api.git

cd fastapi-doctor-patient-api

Replace "YOUR_USERNAME" with your actual GitHub username.

2. Create a Virtual Environment

python -m venv venv

Activate the virtual environment.

Windows:

venv\Scripts\activate

Linux/macOS:

source venv/bin/activate

3. Install Dependencies

pip install -r requirements.txt

4. Configure Environment Variables

Copy ".env.example" to ".env" and configure the database URL and JWT secret key.

5. Start the Application

Run the following command from the project root:

uvicorn app.main:app --reload

The application will start at:

http://127.0.0.1:8000

6. Access API Documentation

FastAPI provides interactive API documentation.

Swagger UI:

http://127.0.0.1:8000/docs

ReDoc:

http://127.0.0.1:8000/redoc

API Testing

Use Swagger UI or Postman to test the available endpoints.

Test the following scenarios:

1. Create and retrieve doctors.
2. Create patients and assign them to doctors.
3. Verify invalid doctor assignment.
4. Update and delete records.
5. Validate duplicate email addresses.
6. Validate phone numbers.
7. Test filtering and pagination.
8. Generate JWT tokens.
9. Access protected endpoints using authentication.

Run Automated Tests

Execute:

pytest -v

Ensure all tests pass before submission.

Screenshots

Add screenshots of successfully tested APIs to a "screenshots/" directory.

Suggested screenshots:

- Doctor creation.
- Patient creation.
- Doctor–Patient relationship.
- Doctor update and soft delete.
- Email and phone validation.
- Filtering and pagination.
- JWT login and authentication.
- Successful pytest execution.

Submission

The final submission should include:

- Complete FastAPI source code.
- GitHub repository.
- README documentation.
- Dependency requirements.
- Database integration.
- JWT authentication.
- Unit tests.
- Swagger or Postman screenshots.

Share the required screenshots in the assigned group after successfully completing and testing the application.

Conclusion

This project demonstrates backend development using FastAPI, including REST API design, relational database management, authentication, validation, modular architecture, testing and containerization.

It provides practical experience in building maintainable and scalable Python backend applications.
