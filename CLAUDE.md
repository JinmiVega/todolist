# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

### Backend (FastAPI)
```bash
# Run backend server
cd backend
python main.py
# OR using uvicorn directly
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### Frontend (Streamlit)
```bash
# Run frontend app
cd frontend
streamlit run main.py
```

### Setup
```bash
# Install dependencies
pip install -r requirements.txt

# Optional: Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

## Architecture Overview

### Backend Structure
- **main.py**: FastAPI app entry point, includes routers
- **api_user.py**: Authentication endpoints (register, login, profile) with JWT tokens
- **api_todo.py**: Todo CRUD endpoints with user authorization
- **Shared utilities**: Database functions (load_db, save_db), JWT verification
- **Database**: JSON file storage at `../db/db.json` relative to backend

Authentication flow:
1. User registers/logs in via api_user.py
2. JWT token generated with user email as subject
3. verify_token dependency extracts email from JWT
4. User ID retrieved from database using email for authorization

### Frontend Structure
- **main.py**: Streamlit app entry point with session state management and navigation
- **auth_screen.py**: Login/register forms with tab interface
- **todo_screen.py**: Todo list management with CRUD operations
- **profile_screen.py**: User profile and todo statistics display
- **api_client.py**: HTTP client for backend communication with automatic JWT headers

Session state management:
- `authenticated`: Boolean login status
- `token`: JWT access token
- `user_email`: Current user's email

### Database Schema
JSON structure in `db/db.json`:
```json
{
  "users": {
    "user_id": {
      "id": "uuid",
      "email": "string",
      "password": "bcrypt_hash"
    }
  },
  "todos": {
    "todo_id": {
      "id": "uuid",
      "title": "string", 
      "description": "string",
      "completed": "boolean",
      "user_id": "uuid",
      "created_at": "iso_datetime"
    }
  }
}
```

### Security Implementation
- Passwords hashed with bcrypt before storage
- JWT tokens expire after 30 minutes 
- All todo endpoints require valid JWT token
- User can only access their own todos (user_id validation)
- SECRET_KEY used for JWT signing (hardcoded - not production ready)

## Important Notes

- Backend runs on port 8000, frontend on port 8501
- Database path inconsistency: backend uses `../db/db.json`, but there's also `backend/db.json`
- No database migrations or schema validation
- Frontend uses st.rerun() after state changes to refresh UI
- API client includes automatic error handling for connection issues