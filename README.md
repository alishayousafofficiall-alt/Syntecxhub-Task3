# 📋 TaskFlow — Full Stack Task Manager App
### SyntecxHub Project 1 | React + Node.js + Express + MongoDB + JWT

---

## 🗂️ Project Structure

```
task-manager/
├── backend/          ← Node.js + Express + MongoDB API
│   ├── controllers/
│   │   ├── authController.js
│   │   └── taskController.js
│   ├── middleware/
│   │   └── auth.js         ← JWT protect middleware
│   ├── models/
│   │   ├── User.js
│   │   └── Task.js
│   ├── routes/
│   │   ├── auth.js
│   │   └── tasks.js
│   ├── server.js
│   ├── .env.example
│   └── package.json
│
└── frontend/         ← React App
    ├── public/
    │   └── index.html
    └── src/
        ├── components/
        │   ├── Navbar.js / .css
        │   ├── TaskCard.js / .css
        │   ├── TaskModal.js
        │   └── PrivateRoute.js
        ├── context/
        │   └── AuthContext.js
        ├── pages/
        │   ├── Login.js
        │   ├── Register.js
        │   ├── Dashboard.js / .css
        │   └── Auth.css
        ├── utils/
        │   └── api.js
        ├── App.js
        ├── index.js
        └── index.css
```

---

## ⚙️ Setup Instructions

### Prerequisites
- Node.js v16+
- MongoDB (local or MongoDB Atlas)
- npm or yarn

---

### 1️⃣ Backend Setup

```bash
cd backend
npm install
```

Create your `.env` file:
```bash
cp .env.example .env
```

Edit `.env`:
```
PORT=5000
MONGO_URI=mongodb://localhost:27017/taskmanager
JWT_SECRET=your_super_secret_key_here
JWT_EXPIRE=7d
NODE_ENV=development
```

Start the backend:
```bash
npm run dev     # development (nodemon)
npm start       # production
```

Backend runs on: `http://localhost:5000`

---

### 2️⃣ Frontend Setup

```bash
cd frontend
npm install
npm start
```

Frontend runs on: `http://localhost:3000`

> The `"proxy": "http://localhost:5000"` in frontend/package.json auto-forwards API calls.

---

## 🔗 API Endpoints

### Auth Routes (`/api/auth`)
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| POST | `/api/auth/register` | Public | Register new user |
| POST | `/api/auth/login` | Public | Login & get JWT |
| GET | `/api/auth/me` | Private | Get logged-in user |

### Task Routes (`/api/tasks`)
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET | `/api/tasks` | Private | Get all my tasks |
| POST | `/api/tasks` | Private | Create new task |
| GET | `/api/tasks/:id` | Private | Get single task |
| PUT | `/api/tasks/:id` | Private | Update task |
| DELETE | `/api/tasks/:id` | Private | Delete task |

### Query Params for GET /api/tasks
- `?status=todo` | `in-progress` | `completed`
- `?priority=low` | `medium` | `high`
- `?search=keyword`

---

## ✨ Features

- ✅ JWT Authentication (register, login, logout)
- ✅ Protected routes (frontend + backend middleware)
- ✅ Full CRUD for tasks
- ✅ Filter by status, priority, search
- ✅ Task status quick-change dropdown
- ✅ Due date with overdue detection
- ✅ Dashboard summary stats
- ✅ Dark violet UI theme
- ✅ Responsive design
- ✅ Toast notifications
- ✅ Input validation (frontend + backend)

---

## 🧰 Tech Stack

| Layer | Tech |
|-------|------|
| Frontend | React 18, React Router v6, Axios |
| Backend | Node.js, Express.js |
| Database | MongoDB + Mongoose |
| Auth | JWT + bcryptjs |
| Validation | express-validator |
| UI | Custom CSS, react-hot-toast, react-icons |

---

## 🔐 JWT Flow

1. User registers/logs in → backend returns JWT token
2. Token stored in `localStorage`
3. Every API request sends `Authorization: Bearer <token>` header
4. Backend `protect` middleware verifies token on all `/api/tasks` routes
5. Unauthorized requests get `401` response
