Mechanic Shop API

-----

Overview

The Mechanic Shop API is a RESTful web service built using Flask, SQLAlchemy, and Marshmallow. It allows users to manage customers, mechanics, and service tickets, including assigning and removing mechanics from service tickets. The project follows the Application Factory Pattern and uses Flask Blueprints to organize routes by resource.

-----

This project demonstrates:

RESTful API design
Flask Application Factory Pattern
SQLAlchemy ORM relationships
Marshmallow schemas for serialization and validation
MySQL database integration
Blueprint-based modular architecture
Testing API endpoints using Postman

-----

Technologies Used

Python 3
Flask
Flask-SQLAlchemy
Flask-Marshmallow
Marshmallow-SQLAlchemy
MySQL
mysql-connector-python
python-dotenv
Postman

-----

Project Structure ***Using REST API Patterns***
mechanic_shop/
│
├── app/
│   ├── __init__.py
│   ├── extensions.py
│   ├── models.py
│   │
│   └── blueprints/
│       ├── customers/
│       │   ├── __init__.py
│       │   ├── routes.py
│       │   └── schemas.py
│       │
│       ├── mechanics/
│       │   ├── __init__.py
│       │   ├── routes.py
│       │   └── schemas.py
│       │
│       └── service_tickets/
│           ├── __init__.py
│           ├── routes.py
│           └── schemas.py
│
├── run.py
├── requirements.txt
├── .env
├── .gitignore
└── Mechanic Shop.postman_collection.json

-----
Database Models

Customer
    Represents a customer of the mechanic shop.
        Fields:
            - id (Primary Key)
            - name
            - email
            - phone_number

    Relationship:
        - One-to-many relationship with ServiceTicket

Mechanic
    Represents a mechanic working at the shop.
        Fields:
            - id (Primary Key)
            - name
            - email
            - phone_number
            - salary

        Relationship:
            - Many-to-many relationship with ServiceTicket

ServiceTicket
    Represents a service request for a vehicle.
        Fields:
           - id (Primary Key)
            - vin
            - service_date
            - description
            - customer_id (Foreign Key)
            
        Relationships:
            - Many-to-one relationship with Customer
            - Many-to-many relationship with Mechanic

-----

Installation Instructions

Step 1: Clone the repository
    git clone https://github.com/YOUR_USERNAME/mechanic_shop.git
    cd mechanic_shop

Step 2: Create virtual environment
    python -m venv venv

Step 3: Activate virtual environment\
    Windows:
        venv\Scripts\activate
    Mac/Linux:
        source venv/bin/activate

Step 4: Install dependencies
    pip install -r requirements.txt

Step 5: Configure environment variables
    Create a .env file in the root directory:
        DATABASE_URL=mysql+mysqlconnector://root:YOUR_PASSWORD@localhost/mechanic_shop_db
        SECRET_KEY=your_secret_key

Step 6: Create MySQL database
    Open MySQL Workbench and run:
        CREATE DATABASE mechanic_shop_db;

Step 7: Run the application
    python run.py
    Server will run at:
        http://127.0.0.1:5000

API Endpoints
    Base URL:
        http://127.0.0.1:5000

Customer Endpoints
    Create Customer
        POST /customers/
        Example Body:
            {
            "name": "John Doe",
            "email": "john@email.com",
            "phone_number": "555-123-4567"
            }

    Get All Customers
        GET /customers/

    Get Customer by ID
        GET /customers/<id>

    Update Customer
        PUT /customers/<id>

    Delete Customer
        DELETE /customers/<id>

Mechanic Endpoints
    Create Mechanic
        POST /mechanics/

    Get All Mechanics
        GET /mechanics/

    Update Mechanic
        PUT /mechanics/<id>

    Delete Mechanic
        DELETE /mechanics/<id>

Service Ticket Endpoints
    Create Service Ticket
        POST /service-tickets/
        Example Body:
            {
            "vin": "1HGCM82633A123456",
            "service_date": "2026-02-06",
            "description": "Oil change",
            "customer_id": 1
            }

    Assign Mechanic
        PUT /service-tickets/<ticket_id>/assign-mechanic/<mechanic_id>

    Remove Mechanic
        PUT /service-tickets/<ticket_id>/remove-mechanic/<mechanic_id>

    Get All Service Tickets
        GET /service-tickets/

-----

Application Factory Pattern
    This project uses the Flask Application Factory Pattern to allow modular configuration and scalability.
        Benefits:
        - Cleaner architecture
        - Easier testing
        - Avoids circular imports
        - Supports multiple environments

-----

Marshmallow Schemas
    Marshmallow is used to:
        - Serialize database objects into JSON
        - Deserialize JSON into Python objects
        - Validate input data
    SQLAlchemyAutoSchema automatically generates schemas from models.
 
-----

Testing with Postman
    This project includes a Postman collection file:
        Mechanic Shop.postman_collection.json
    
    Import into Postman:
    1. Open Postman
    2. Click Import
    3. Select the JSON file
    4. Run requests

-----

Author
Kayla Salmon