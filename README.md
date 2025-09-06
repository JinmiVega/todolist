# Todo List Application

Una aplicación completa de lista de tareas con FastAPI backend y Streamlit frontend, organizada en carpetas separadas.

## Características

- **Backend FastAPI**: API REST con autenticación JWT
- **Frontend Streamlit**: Interfaz web interactiva modular
- **Base de datos local**: Almacenamiento en archivo JSON
- **Autenticación**: Login/Register con tokens JWT
- **CRUD completo**: Crear, leer, actualizar y eliminar tareas

## Estructura del Proyecto

```
├── backend/
│   ├── main.py          # API FastAPI
│   └── db.json          # Base de datos local
├── frontend/
│   ├── main.py          # Aplicación principal Streamlit
│   ├── api_client.py    # Cliente API
│   ├── auth_screen.py   # Pantalla Login/Register
│   ├── todo_screen.py   # Pantalla Lista de Tareas
│   └── profile_screen.py # Pantalla Perfil
├── requirements.txt     # Dependencias
└── README.md           # Este archivo
```

## Instalación

0. Crea un entorno virtual (opcional pero recomendado):
```
python -m venv venv
source venv/bin/activate 
# En Windows : 
source venv/Scripts/activate

```

1. Instalar dependencias:
```bash
pip install -r requirements.txt
```

## Uso

### 1. Ejecutar el Backend (FastAPI)

```bash
cd backend
python main.py
```

### 1.1 usando uvicorn directamente:
```bash
cd backend
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

El API estará disponible en: http://localhost:8000

### 2. Ejecutar el Frontend (Streamlit)

En otra terminal:
```bash
cd frontend
streamlit run main.py
```

La aplicación web estará disponible en: http://localhost:8501

## API Endpoints

### Autenticación
- `POST /register` - Registrar nuevo usuario
- `POST /login` - Iniciar sesión
- `GET /profile` - Obtener perfil del usuario

### Todos
- `GET /todos` - Obtener todas las tareas del usuario
- `POST /todos` - Crear nueva tarea
- `GET /todos/{todo_id}` - Obtener tarea específica
- `PUT /todos/{todo_id}` - Actualizar tarea
- `DELETE /todos/{todo_id}` - Eliminar tarea

## Uso de la Aplicación

1. **Registro/Login**: Crea una cuenta o inicia sesión
2. **Lista de Tareas**: Agrega, completa y elimina tareas
3. **Perfil**: Ve estadísticas de tus tareas

## Funcionalidades

### Backend
- Autenticación JWT con tokens seguros
- Validación de datos con Pydantic
- Hash seguro de contraseñas con bcrypt
- CRUD completo para usuarios y tareas
- Autorización por usuario

### Frontend (Modular)
- **main.py**: Aplicación principal y navegación
- **auth_screen.py**: Login y registro de usuarios
- **todo_screen.py**: Gestión completa de tareas
- **profile_screen.py**: Perfil de usuario y estadísticas
- **api_client.py**: Cliente para comunicación con API

## Seguridad

- Contraseñas hasheadas con bcrypt
- Tokens JWT para autenticación
- Autorización por usuario para acceso a tareas
- Validación de entrada de datos