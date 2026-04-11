<div align="center">

<img src="https://img.shields.io/badge/OnTrack-Task%20Manager-4F46E5?style=for-the-badge&logo=checkmarx&logoColor=white" alt="OnTrack" />

# OnTrack — Task Manager

**A full-stack task management application built with React, Express, and MongoDB.**

[![React](https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react)](https://reactjs.org/) [![Vite](https://img.shields.io/badge/Vite-5-646CFF?style=flat-square&logo=vite)](https://vitejs.dev/) [![Express](https://img.shields.io/badge/Express-4-000000?style=flat-square&logo=express)](https://expressjs.com/) [![MongoDB](https://img.shields.io/badge/MongoDB-7-47A248?style=flat-square&logo=mongodb)](https://www.mongodb.com/) [![Node.js](https://img.shields.io/badge/Node.js-20+-339933?style=flat-square&logo=node.js)](https://nodejs.org/) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](./LICENSE)

[Features](#-features) · [Getting Started](#-getting-started) · [Project Structure](#-project-structure) · [API Reference](#-api-reference) · [Environment Variables](#-environment-variables)

</div>

---

## Overview

**OnTrack** is a productivity-focused task manager that allows users to create, organize, and track tasks with ease. It features JWT-based authentication, a responsive React frontend powered by Vite, and a RESTful Express API backed by MongoDB.

---

## Features

- **Authentication** — Secure sign-up / login with JWT tokens and hashed passwords (bcrypt)
- **Task CRUD** — Create, read, update, and delete tasks
- **Task Status** — Track tasks as `Todo`, `In Progress`, or `Done`
- **Priority Levels** — Assign `Low`, `Medium`, or `High` priority to each task
- **Due Dates** — Set deadlines and receive overdue indicators
- **Filtering & Sorting** — Filter tasks by status, priority, or due date
- **User Isolation** — Each user only sees their own tasks
- **Responsive UI** — Works seamlessly on desktop and mobile

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 18 + Vite |
| Styling | CSS Modules / Tailwind CSS |
| Backend | Node.js + Express 4 |
| Database | MongoDB + Mongoose |
| Auth | JSON Web Tokens (JWT) + bcrypt |
| Dev Tools | ESLint, Nodemon, dotenv |

---

## Project Structure

```
OnTrack/
├── frontend/                   # React + Vite application
│   ├── public/
│   ├── src/
│   │   ├── assets/
│   │   ├── components/         # Reusable UI components
│   │   │   ├── TaskCard.jsx
│   │   │   ├── TaskForm.jsx
│   │   │   └── Navbar.jsx
│   │   ├── pages/              # Route-level pages
│   │   │   ├── Login.jsx
│   │   │   ├── Register.jsx
│   │   │   └── Dashboard.jsx
│   │   ├── services/           # Axios API calls
│   │   │   └── api.js
│   │   ├── context/            # React context (Auth)
│   │   │   └── AuthContext.jsx
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── .env                    # Frontend env variables
│   ├── index.html
│   ├── vite.config.js
│   └── package.json
│
├── backend/                    # Express REST API
│   ├── config/
│   │   └── db.js               # MongoDB connection
│   ├── controllers/
│   │   ├── authController.js
│   │   └── taskController.js
│   ├── middleware/
│   │   └── authMiddleware.js   # JWT verification
│   ├── models/
│   │   ├── User.js
│   │   └── Task.js
│   ├── routes/
│   │   ├── authRoutes.js
│   │   └── taskRoutes.js
│   ├── .env                    # Backend env variables
│   ├── server.js
│   └── package.json
│
└── README.md
```

---

## Getting Started

### Prerequisites

- **Node.js** v20 or higher
- **MongoDB** running locally or a [MongoDB Atlas](https://www.mongodb.com/atlas) cluster
- **npm** or **yarn**

---

### 1. Clone the repository

```bash
git clone https://github.com/RAZAFITSALAMA-sandra/OnTrack.git
cd OnTrack
```

---

### 2. Configure environment variables

#### Backend — `backend/.env`

```env
PORT=3000
MONGO_URI=mongodb://admin:sandra@localhost:27017/taskflow?authSource=admin
JWT_SECRET=taskflow_secret_2024
```

<!-- #### Frontend — `frontend/.env`

```env
VITE_API_URL=http://localhost:3000/api
```

> **Security note:** Never commit `.env` files to version control. Both are already listed in `.gitignore`. -->

---

### 3. Install dependencies

```bash
# Backend
cd backend
npm install

# Frontend
cd ../frontend
npm install
```

---

### 4. Start the development servers

**Backend** (runs on `http://localhost:3000`)

```bash
cd backend
npm run dev
```

**Frontend** (runs on `http://localhost:5173`)

```bash
cd frontend
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) in your browser.

---

### 5. Build for production

```bash
# Build the frontend
cd frontend
npm run build

# Start the backend in production mode
cd ../backend
npm start
```

> The compiled frontend assets will be in `frontend/dist/`. You can serve them statically from Express or deploy them separately (Vercel, Netlify, etc.).

---

## Environment Variables

| Variable | Location | Description |
|---|---|---|
| `PORT` | `backend/.env` | Port the Express server listens on |
| `MONGO_URI` | `backend/.env` | Full MongoDB connection string |
| `JWT_SECRET` | `backend/.env` | Secret key used to sign JWT tokens |
<!-- | `VITE_API_URL` | `frontend/.env` | Base URL of the backend API | -->

---

## API Reference

All endpoints are prefixed with `/api`.  
Protected routes require a `Authorization: Bearer <token>` header.

### Auth

| Method | Endpoint | Access | Description |
|---|---|---|---|
| `POST` | `/api/auth/register` | Public | Create a new account |
| `POST` | `/api/auth/login` | Public | Log in and receive a JWT |
| `GET` | `/api/auth/me` | Protected | Get current user info |

### Tasks

| Method | Endpoint | Access | Description |
|---|---|---|---|
| `GET` | `/api/tasks` | Protected | Get all tasks for the logged-in user |
| `POST` | `/api/tasks` | Protected | Create a new task |
| `GET` | `/api/tasks/:id` | Protected | Get a single task by ID |
| `PUT` | `/api/tasks/:id` | Protected | Update a task |
| `DELETE` | `/api/tasks/:id` | Protected | Delete a task |

### Example — Create a task

**Request**
```http
POST /api/tasks
Authorization: Bearer <your_jwt_token>
Content-Type: application/json

{
  "title": "Write project documentation",
  "description": "Cover setup, API, and deployment.",
  "status": "todo",
  "priority": "high",
  "dueDate": "2024-12-31"
}
```

**Response `201 Created`**
```json
{
  "_id": "64f3a1c2e4b0c72d88f1a9d3",
  "title": "Write project documentation",
  "description": "Cover setup, API, and deployment.",
  "status": "todo",
  "priority": "high",
  "dueDate": "2024-12-31T00:00:00.000Z",
  "user": "64f3a0e1e4b0c72d88f1a9c1",
  "createdAt": "2024-09-03T10:22:42.000Z",
  "updatedAt": "2024-09-03T10:22:42.000Z"
}
```

---

## Data Models

### User

```js
{
  name:      String,   // required
  email:     String,   // required, unique
  password:  String,   // hashed with bcrypt
  createdAt: Date
}
```

### Task

```js
{
  title:       String,                          // required
  description: String,
  status:      enum ['todo', 'in-progress', 'done'],   // default: 'todo'
  priority:    enum ['low', 'medium', 'high'],         // default: 'medium'
  dueDate:     Date,
  user:        ObjectId (ref: 'User'),          // required
  createdAt:   Date,
  updatedAt:   Date
}
```

---

## Scripts

### Backend

| Script | Command | Description |
|---|---|---|
| `dev` | `nodemon server.js` | Start with hot reload |
| `start` | `node server.js` | Start in production mode |

### Frontend

| Script | Command | Description |
|---|---|---|
| `dev` | `vite` | Start the dev server |
| `build` | `vite build` | Build for production |
| `preview` | `vite preview` | Preview the production build |
| `lint` | `eslint src` | Run ESLint |

---

## Deployment

### Backend (Railway / Render / VPS)

1. Set environment variables (`PORT`, `MONGO_URI`, `JWT_SECRET`) in your hosting dashboard.
2. Push your code or connect your GitHub repository.
3. The start command is `node server.js`.

### Frontend (Vercel / Netlify)

1. Set `VITE_API_URL` to your deployed backend URL.
2. Build command: `npm run build`
3. Publish directory: `dist`

### MongoDB (Atlas)

Replace `MONGO_URI` with your Atlas connection string:
```
mongodb+srv://<user>:<password>@cluster0.xxxxx.mongodb.net/taskflow?retryWrites=true&w=majority
```

---

## Contributing

Contributions are welcome!

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m "feat: add my feature"`
4. Push to the branch: `git push origin feature/my-feature`
5. Open a Pull Request

Please follow the [Conventional Commits](https://www.conventionalcommits.org/) specification.

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---