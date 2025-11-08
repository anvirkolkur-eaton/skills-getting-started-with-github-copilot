# Build Instructions

This document describes how to build and run the Mergington High School Activities application.

## Prerequisites

- Python 3.8 or higher
- pip (Python package manager)

## Build Steps

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

This will install:
- `fastapi` - Web framework for building APIs
- `uvicorn` - ASGI server for running FastAPI applications
- `pytest` - Testing framework
- `httpx` - HTTP client for testing

### 2. Verify Installation

```bash
python -c "import fastapi, uvicorn, pytest, httpx; print('All dependencies installed successfully')"
```

### 3. Run the Application

#### Option A: Using Python directly
```bash
python src/app.py
```

#### Option B: Using uvicorn
```bash
uvicorn src.app:app --host 0.0.0.0 --port 8000
```

The application will be available at:
- Main page: http://localhost:8000/
- API documentation: http://localhost:8000/docs
- Alternative API docs: http://localhost:8000/redoc

## Testing

### Run Tests
```bash
pytest
```

### Test API Manually
```bash
# Get all activities
curl http://localhost:8000/activities

# Sign up for an activity
curl -X POST "http://localhost:8000/activities/Chess%20Club/signup?email=student@mergington.edu"
```

## Build Verification

To verify the build is successful, run:

```bash
# Import check
python -c "from src.app import app; print('Build successful!')"

# Quick API test
python -c "
from src.app import app
from fastapi.testclient import TestClient
client = TestClient(app)
response = client.get('/activities')
assert response.status_code == 200
print('API is working correctly!')
"
```

## Common Issues

### ModuleNotFoundError
If you get a `ModuleNotFoundError`, make sure you've installed all dependencies:
```bash
pip install -r requirements.txt
```

### Port Already in Use
If port 8000 is already in use, you can run the app on a different port:
```bash
uvicorn src.app:app --host 0.0.0.0 --port 8080
```

## Development

For development with auto-reload:
```bash
uvicorn src.app:app --reload
```

This will automatically restart the server when you make changes to the code.
