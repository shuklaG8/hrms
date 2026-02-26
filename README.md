# Human Resources Management System (HRMS)

## Project Overview
This HRMS (Human Resources Management System) is a comprehensive full-stack application designed to streamline employee management and attendance tracking. It consists of a Django-based backend providing a robust REST API, and a modern React frontend offering an intuitive user interface for managing employee data, roles, and daily attendance records.

## Tech Stack Used
### Backend
- **Framework:** Django & Django REST Framework (DRF)
- **Database:** SQLite (local development) / PostgreSQL (production via Render/Railway)
- **Language:** Python 3.x
- **Configuration:** python-dotenv, dj-database-url (for environment management), WhiteNoise (for static file serving)

### Frontend
- **Framework:** React 19 (managed via Vite)
- **Styling:** Tailwind CSS 4
- **Icons:** Lucide-React
- **Routing:** React Router DOM (v7)
- **HTTP Client:** Axios

---

## Steps to Run the Project Locally

### Prerequisites
- Python (3.9+)
- Node.js (v18+)

### 1. Backend Setup (Django)
1. Open a terminal and navigate to the backend directory:
   ```bash
   cd backend
   ```
2. Create and activate a virtual environment (optional but recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
3. Install the Python dependencies:
   ```bash
   pip install -r requirements.txt
   # Ensure these are installed: djangorestframework, django-cors-headers, dj-database-url, whitenoise
   ```
4. Apply the database migrations to set up your local SQLite database:
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```
5. Create an admin superuser to manage the system:
   ```bash
   python create_superuser.py
   # Alternatively: python manage.py createsuperuser
   ```
6. Start the Django development server:
   ```bash
   python manage.py runserver
   ```
   *The backend will now be running on `http://127.0.0.1:8000/`*

### 2. Frontend Setup (React/Vite)
1. Open a new terminal and navigate to the frontend directory:
   ```bash
   cd frontend
   ```
2. Install the Node.js packages:
   ```bash
   npm install
   ```
3. Create a `.env` file in the root of the `frontend` folder and add the backend API URL:
   ```env
   VITE_API_KEY="http://127.0.0.1:8000"
   ```
   *(Make sure to point this back to your production server if you plan to build for production.)*
4. Start the Vite development server:
   ```bash
   npm run dev
   ```
   *The frontend will compile and typically run on `http://localhost:5173/`*

---

## Assumptions and Limitations
- **Database Connection:** The backend uses `dj_database_url` to automatically configure the database. It defaults to a local SQLite database (`db.sqlite3`) for development but can seamlessly switch to PostgreSQL in production (Render/Railway) by providing a `DATABASE_URL` environment variable.
- **CORS Allow Origins:** The Django backend has `CORS_ALLOW_ALL_ORIGINS = True` enabled for effortless development and deployed React connections. For strict production environments, this should be scoped down to specific trusted domains.
- **Authentication:** Currently, administrative tasks assume the existence of the `admin` user account created by the system setup script. Further role-based access control (RBAC) might require expansion on the `Employee` models.
- **Strict Mode:** React's `<StrictMode>` was disabled in development to prevent duplicate development-only API network calls.
