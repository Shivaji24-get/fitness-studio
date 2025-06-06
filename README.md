# 🏋️ Fitness Studio Booking API

A FastAPI-based backend service for managing fitness class bookings with timezone support, built with Python 3.13.

## 🚀 Quick Start

1. **Prerequisites**
   - Windows OS (tested on Windows 10/11)
   - Python 3.13 or higher
   - Git (optional)

2. **Clone the repository** (if not already done)
   ```bash
   git clone <repository-url>
   cd fitness_studio
   ```

3. **Run the application**
   Simply double-click on `run.bat` or run it from the command line:
   ```bash
   .\run.bat
   ```
   This will:
   - Create a virtual environment (if it doesn't exist)
   - Install all required dependencies
   - Run database migrations
   - Start the development server
   - Open the API documentation in your default browser

### 🛠️ Manual Setup (Alternative to run.bat)

1. **Create and activate a virtual environment**
   ```bash
   python -m venv venv
   .\venv\Scripts\activate
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up environment variables**
   Create a `.env` file in the project root with the following content:
   ```
   # Database configuration
   DATABASE_URL=sqlite:///./fitness_studio.db
   
   # Application settings
   DEBUG=True
   SECRET_KEY=your-secret-key-here
   ```

4. **Run the application**
   ```bash
   uvicorn app.main:app --reload
   ```
   This will start the development server with auto-reload enabled.

4. **Access the application**
   - API Documentation (Swagger UI): http://127.0.0.1:8000/docs
   - Alternative Documentation (ReDoc): http://127.0.0.1:8000/redoc
   - API Base URL: http://127.0.0.1:8000/api/v1

## ✨ Features

- **Class Management**
  - Create and list fitness classes
  - Set class schedules with timezone support (IST/UTC)
  - Track available slots and capacity

- **Booking System**
  - Book and cancel class spots
  - View user bookings
  - Prevent double bookings and handle full classes

- **API Features**
  - RESTful API design
  - Input validation with Pydantic
  - Comprehensive error handling
  - Request/response logging
  - API versioning (v1)

## 🏗️ Project Structure

```
fitness_studio/
├── app/                           # Main application package
│   ├── __init__.py
│   ├── api/                       # API layer
│   │   └── v1/                    # API version 1
│   │       ├── endpoints/         # API endpoints
│   │       │   ├── __init__.py
│   │       │   ├── classes.py     # Class endpoints
│   │       │   └── bookings.py    # Booking endpoints
│   │       └── __init__.py
│   │
│   ├── models/                   # Database models
│   │   ├── __init__.py
│   │   └── *.py                  # Model definitions
│   │
│   ├── schemas/                 # Pydantic schemas
│   │   ├── __init__.py
│   │   ├── base.py               # Base schemas
│   │   ├── class_schema.py       # Class schemas
│   │   └── booking_schema.py     # Booking schemas
│   │
│   ├── services/                # Business logic
│   │   ├── __init__.py
│   │   ├── class_service.py     # Class business logic
│   │   └── booking_service.py   # Booking business logic
│   │
│   ├── utils/                   # Utility functions
│   │   └── logger.py            # Logging configuration
│   │
│   ├── config.py               # Application configuration
│   └── database.py              # Database configuration
│
├── tests/                      # Test files
│   ├── __init__.py
│   ├── conftest.py              # Test fixtures
│   ├── integration/             # Integration tests
│   └── unit/                    # Unit tests
│
├── data/                       # Data files
│   └── fitness_studio.db        # SQLite database (development)
│
├── logs/                       # Application logs
├── requirements.txt             # Project dependencies
├── pytest.ini                  # Pytest configuration
│   │   └── README.md                   # This file

## 🛠️ Setup and Installation

### Prerequisites
- Windows 10/11 (tested) or any OS with Python 3.13+
- Python 3.13 or higher
- pip (Python package manager)
- SQLite (included with Python)

### Clone the Repository
```bash
git clone <repository-url>
cd fitness_studio
```

### Windows Setup
1. **Run the setup script** (recommended):
   ```bash
   .\run.bat
   ```
   This will automatically:
   - Create a virtual environment
   - Install all dependencies
   - Set up the database
   - Start the development server

2. **Manual Setup** (if needed):
   ```bash
   # Create and activate virtual environment
   python -m venv venv_new
   .\venv_new\Scripts\activate

   # Install dependencies
   pip install -r requirements.txt

   # Set up environment variables
   echo DATABASE_URL=sqlite:///./data/fitness_studio.db > .env
   echo LOG_LEVEL=INFO >> .env

   # Initialize the database
   python -c "from fitness_studio.app.database import init_db; init_db()"
   ```

### Environment Variables
Create a `.env` file in the project root with the following variables:
```
DATABASE_URL=sqlite:///./data/fitness_studio.db
LOG_LEVEL=INFO
# Uncomment and set these for production:
# SECRET_KEY=your-secret-key-here
# DEBUG=False
```

## 🚀 Running the Application

### Development
1. **Using run.bat (Recommended)**
   ```bash
   .\run.bat
   ```
   This will start the development server with auto-reload enabled.

2. **Manual Setup**
   If you prefer not to use run.bat, you can follow the manual setup instructions in the [Quick Start](#-quick-start) section above.

2. **Manual Start**
   ```bash
   # Activate virtual environment (if not already activated)
   .\venv_new\Scripts\activate
   
   # Start the development server
   uvicorn fitness_studio.main:app --reload
   ```

3. **Production** (Using Uvicorn with workers)
   ```bash
   uvicorn fitness_studio.main:app --host 0.0.0.0 --port 8000 --workers 4
   ```

### API Endpoints
- Swagger UI (Interactive Docs): http://127.0.0.1:8000/docs
- ReDoc (Alternative Docs): http://127.0.0.1:8000/redoc
- API Base URL: http://127.0.0.1:8000/api/v1

## 🧪 Running Tests

### Prerequisites
Make sure you have the development dependencies installed:
```bash
pip install -r requirements.txt
```

### Running Tests

1. **Run all tests** (unit + integration)
   ```bash
   .\venv_new\Scripts\pytest -v
   ```

2. **Run unit tests only**
   ```bash
   .\venv_new\Scripts\pytest tests/unit -v
   ```

3. **Run integration tests**
   ```bash
   .\venv_new\Scripts\pytest tests/integration -v
   ```

4. **Run with coverage report**
   ```bash
   .\venv_new\Scripts\pytest --cov=fitness_studio --cov-report=term-missing
   ```

5. **Run tests with detailed logging**
   ```bash
   .\venv_new\Scripts\pytest -v --log-cli-level=INFO
   ```

### Test Structure
- `tests/unit/`: Unit tests for individual components
- `tests/integration/`: Integration tests for API endpoints
- `conftest.py`: Test fixtures and configuration
- `pytest.ini`: Pytest configuration

## 📚 API Documentation

### Classes

#### Create a Class
```http
POST /api/v1/classes/classes
Content-Type: application/json

{
  "name": "Morning Yoga",
  "instructor": "Jane Doe",
  "total_slots": 10,
  "datetime_ist": "2025-06-10T09:00:00+05:30",
  "duration_minutes": 60
}
```

#### List All Classes
```http
GET /api/v1/classes/classes?include_past=false
```

### Bookings

#### Create a Booking
```http
POST /api/v1/bookings/bookings
Content-Type: application/json

{
  "class_id": 1,
  "client_name": "John Doe",
  "client_email": "john@example.com"
}
```

#### Get User Bookings
```http
GET /api/v1/bookings/bookings?email=john@example.com
```

#### Cancel a Booking
```http
DELETE /api/v1/bookings/bookings/{booking_id}?email=john@example.com
```

## 🧰 Development

### Code Style
- Follow PEP 8 guidelines
- Use type hints for better code clarity
- Keep functions small and focused

### Git Workflow
1. Create a new branch for your feature/fix:
   ```bash
   git checkout -b feature/your-feature-name
   ```
2. Make your changes and commit:
   ```bash
   git add .
   git commit -m "Add your commit message"
   ```
3. Push your changes and create a pull request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- FastAPI for the awesome web framework
- SQLAlchemy for the ORM
- Pydantic for data validation
- Pytest for testing
│   │
│   ├── utils/                   # Utility functions
│   │   ├── __init__.py
│   │   ├── datetime_utils.py     # Date/time utilities
│   │   └── logger.py             # Logging configuration
│   │
│   ├── __init__.py              # Application package
│   ├── database.py               # Database configuration
│   └── main.py                   # Application entry point
│
├── tests/                      # Test files
│   └── test_classes.py           # Class endpoint tests
│
├── .env                       # Environment variables
├── .gitignore                  # Git ignore file
├── requirements.txt            # Project dependencies
├── README.md                   # This file
└── pyproject.toml              # Project metadata
```

## 🛠️ Setup and Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd fitness_studio
   ```

2. **Set up a virtual environment** (recommended)
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: .\venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**
   - Copy `.env.example` to `.env`
   - Update the configuration as needed

5. **Run the application**
   ```bash
   uvicorn app.main:app --reload
   ```

6. **Access the API documentation**
   - Swagger UI: http://[localhost:8000](http://127.0.0.1:8000/)/docs
   - ReDoc: http://[localhost:8000](http://127.0.0.1:8000/)/redoc

## 🧪 Running Tests

```bash
# Run all tests
python -m pytest

# Run tests with coverage
pytest --cov=app tests/

# Generate HTML coverage report
pytest --cov=app --cov-report=html tests/
```

## 📝 API Documentation

Once the application is running, you can access:

- **Interactive API Docs**: http://localhost:8000/docs
- **Alternative Documentation**: http://localhost:8000/redoc
http://127.0.0.1:8000/

## 📦 Dependencies

- FastAPI - Modern, fast web framework
- SQLAlchemy - SQL toolkit and ORM
- Pydantic - Data validation
- python-dotenv - Environment variable management
- pytest - Testing framework

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<div align="center">
  <p>Made with ❤️ for fitness enthusiasts</p>
  <small>Built with FastAPI and Python</small>
</div>
