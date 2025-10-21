# Web Engineering Project

A secure authentication system demonstrating industry best practices for password hashing and token-based authentication.

---

## 🧠 About

This project implements a robust authentication system with modern security practices. It features **Argon2** password hashing (winner of the Password Hashing Competition) and a JWT-based authentication flow with refresh token rotation to prevent token theft and replay attacks.

The application consists of a .NET backend API and a frontend client, demonstrating secure communication patterns and proper credential management.

---

## ✨ Features

- 🔐 **Argon2 Password Hashing** - State-of-the-art password storage
- 🎫 **JWT Authentication** - Stateless token-based auth
- 🔄 **Refresh Token Rotation** - Enhanced security against token theft
- 🛡️ **CORS Protection** - Configured for specific frontend origins
- 💾 **SQL Server Integration** - Persistent data storage

---

## 🛠️ Tech Stack

**Backend:**
- .NET (C#)
- ASP.NET Core Web API
- SQL Server
- Argon2 (via compatible library)
- JWT (JSON Web Tokens)

**Frontend:**
- HTML/CSS/JavaScript
- Fetch API for HTTP requests

---

## 📋 Prerequisites

Before running this project, ensure you have:

- [.NET SDK](https://dotnet.microsoft.com/download) (version 6.0 or higher)
- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) (Express or Developer Edition)
- A code editor (VS Code, Visual Studio, etc.)
- Basic knowledge of C# and web development

---

## 🚀 Installation

1. **Clone the repository**
```bash
   git clone https://github.com/GEMIv1/web_engineering_project.git
   cd web_engineering_project
```

2. **Set up the database**
   - Open SQL Server Management Studio (SSMS)
   - Create a new database named `Identity`
   - Run any migration scripts found in the `Database` folder (if available)

3. **Install backend dependencies**
```bash
   cd backend
   dotnet restore
```

---

## ⚙️ Configuration

Create a `.env` file or configure your environment variables:
```env
# Backend Server Configuration
PORT=5121

# Frontend URL (for CORS)
FRONTEND_URL=http://127.0.0.1:5502

# Database Configuration (SQL Server)
DB_SERVER=localhost
DB_PORT=1433
DB_TRUSTED_CONNECTION=true
DB_NAME=Identity

# JWT Configuration
JWT_SECRET=your-secret-key-here-change-in-production
JWT_EXPIRES_IN=15m
```

> ⚠️ **Security Note**: Never commit your `.env` file or expose your `JWT_SECRET` in production!

---

## 💻 Usage

### Running the Backend

Navigate to the backend directory and start the server:
```bash
cd backend
dotnet run
```

The API will be available at `http://localhost:5121`

### Running the Frontend

Open the frontend with a local development server:
```bash
cd frontend
# Using Python
python -m http.server 5502

# Or using Node.js http-server
npx http-server -p 5502
```

Then open your browser and navigate to `http://127.0.0.1:5502`

---

## 📁 Project Structure
```
web_engineering_project/
├── backend/
│   ├── Controllers/          # API endpoint controllers
│   ├── Models/              # Data models
│   ├── Services/            # Business logic (hashing, JWT, etc.)
│   ├── Data/                # Database context
│   ├── Program.cs           # Application entry point
│   └── appsettings.json     # Configuration
├── frontend/
│   ├── index.html           # Main page
│   ├── login.html           # Login page
│   ├── register.html        # Registration page
│   ├── css/                 # Stylesheets
│   └── js/                  # JavaScript files
└── README.md
```

---

## 🔒 Security Features

### Argon2 Password Hashing
- **Memory-hard algorithm** resistant to GPU attacks
- Configurable cost parameters (time, memory, parallelism)
- Produces unique hashes even for identical passwords (via salt)

### JWT with Refresh Token Rotation
- **Access Tokens**: Short-lived (15 minutes) for API requests
- **Refresh Tokens**: Long-lived (7 days) for obtaining new access tokens
- **Automatic Rotation**: Old refresh tokens are invalidated when new ones are issued
- **Secure Storage**: Tokens stored securely on the client side

### Additional Security Measures
- CORS configured to accept requests only from trusted origins
- HTTPS recommended for production deployment
- SQL injection prevention through parameterized queries
- Input validation on all endpoints

---

## 🔌 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register a new user |
| POST | `/api/auth/login` | Login and receive tokens |
| POST | `/api/auth/refresh` | Get new access token using refresh token |
| POST | `/api/auth/logout` | Invalidate refresh token |
| GET | `/api/user/profile` | Get user profile (requires auth) |

### Example Request

**Register:**
```json
POST /api/auth/register
Content-Type: application/json

{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "SecurePassword123!"
}
```

**Login:**
```json
POST /api/auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "SecurePassword123!"
}
```

---

## 🙏 Acknowledgments

- [Argon2](https://github.com/P-H-C/phc-winner-argon2) - Password Hashing Competition winner
- [JWT.io](https://jwt.io/) - JWT implementation resources
