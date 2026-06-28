# MERN Task Tracker Application

A full-stack Task Tracker application built using the MERN stack — MongoDB, Express.js, React.js, and Node.js. The application lets users create, view, update, and delete tasks on a Kanban-style board with drag-and-drop support.

## Live Application

- Frontend: [https://coll-edge-connect-assignment.vercel.app](https://coll-edge-connect-assignment.vercel.app)
- Backend: [https://colledge-connect-assignment-kyvm.onrender.com](https://colledge-connect-assignment-kyvm.onrender.com)
- Tasks API: [https://colledge-connect-assignment-kyvm.onrender.com/api/v1/tasks](https://colledge-connect-assignment-kyvm.onrender.com/api/v1/tasks)

The frontend is deployed on Vercel and the backend on Render's free tier. The initial backend request may take 30–60 seconds if the server has been inactive.

## Assignment Compliance

| Requirement | Implementation |
| --- | --- |
| Create tasks | Validated modal form sends a POST request to the API |
| View tasks | Tasks fetched from MongoDB and displayed in Kanban columns with a details modal |
| Update tasks | Edit task fields or update status via drag and drop |
| Delete tasks | Delete tasks from the UI and database |
| Form validation | Client-side validation with React Hook Form and Zod; backend validation with Mongoose and `runValidators: true` |
| REST APIs | GET, POST, PUT, and DELETE endpoints built with Express |
| MongoDB integration | Mongoose models and queries for all data storage and retrieval |
| Responsive UI | Tailwind CSS responsive utilities for mobile and desktop layouts |
| Dynamic updates | Redux state updates after every CRUD operation — no page refresh |
| Public deployment | Frontend on Vercel, backend on Render |

## Tech Stack

### Frontend

- React 18 + Vite
- Redux Toolkit and React Redux
- React Router
- Axios
- React Hook Form + Zod
- TanStack React Query
- Tailwind CSS
- React Beautiful DnD
- React Toastify
- Firebase Authentication
- Lucide React and React Icons

### Backend

- Node.js
- Express.js
- MongoDB + Mongoose
- JSON Web Token (JWT)
- bcrypt.js
- Cookie Parser
- CORS
- dotenv

## Features

### Task Management
- Create tasks using a validated modal form
- View all tasks on a Kanban board with three columns: **To Do**, **In Progress**, **Done**
- Open a task to view full details
- Edit title, description, status, priority, and due date
- Drag and drop tasks between columns to update status
- Delete tasks
- All data persisted in MongoDB

### Task Organization
- Search tasks by title or description
- Sort by most recent or alphabetical order
- Priority levels: **Low**, **Medium**, **High**
- Optional due dates

### Form Validation

Task rules enforced on both frontend and backend:
- Title is required, 3–100 characters
- Description is optional, max 500 characters
- Status must be `To Do`, `In Progress`, or `Done`
- Priority must be `Low`, `Medium`, or `High`
- Due date is optional

Authentication forms use React Hook Form and Zod to validate name, email format, password length, and password confirmation.

### Authentication (Bonus)
- User registration and login
- Password hashing with bcrypt
- JWT stored in HTTP-only cookies
- Google OAuth via Firebase
- Protected client-side routes
- Logout

> Note: Task API endpoints are currently public. Authentication middleware is implemented but disabled on the task router.

### UI and State
- Responsive layout for mobile and desktop
- Loading indicators during data fetch
- Toast notifications for user actions
- Reusable React components
- Redux Toolkit for global state management
- Optimistic UI updates via React Query

## Project Structure

```
CollEdge_Connect_Assignment/
├── backend/
│   ├── controllers/
│   │   ├── taskController.js
│   │   └── userController.js
│   ├── db/
│   │   └── connectDatabase.js
│   ├── middlewares/
│   │   ├── asyncHandler.js
│   │   └── authMiddleware.js
│   ├── models/
│   │   ├── Task.js
│   │   └── User.js
│   ├── routes/
│   │   ├── taskRoutes.js
│   │   └── userRoutes.js
│   ├── utils/
│   │   └── generateToken.js
│   ├── package.json
│   └── server.js
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── redux/
│   │   ├── App.jsx
│   │   ├── firebase.js
│   │   └── main.jsx
│   ├── package.json
│   ├── tailwind.config.js
│   └── vite.config.js
└── README.md
```

## REST API Reference

Base URL (local): `http://localhost:3000/api/v1`  
Base URL (production): `https://colledge-connect-assignment-kyvm.onrender.com/api/v1`

### Task Endpoints

| Method | Endpoint | Description | Status |
| --- | --- | --- | --- |
| `GET` | `/tasks` | Get all tasks | `200 OK` |
| `POST` | `/tasks` | Create a task | `201 Created` |
| `PUT` | `/tasks/:id` | Update a task | `200 OK` |
| `PUT` | `/tasks/reorder` | Update multiple task statuses | `200 OK` |
| `DELETE` | `/tasks/:id` | Delete a task | `200 OK` |

### User Endpoints

| Method | Endpoint | Description |
| --- | --- | --- |
| `POST` | `/user/signup` | Register a new user |
| `POST` | `/user/login` | Log in with email and password |
| `POST` | `/user/logout` | Log out and clear the cookie |
| `POST` | `/user/google` | Authenticate with Google |

### Task Data Format

```json
{
  "title": "Complete assignment",
  "description": "Test the application and prepare the submission",
  "status": "In Progress",
  "priority": "High",
  "dueDate": "2026-07-01"
}
```

MongoDB automatically adds `_id`, `createdAt`, and `updatedAt`.

## How It Works

```
React (Vite)
     │
     │  Axios HTTP requests
     ▼
Express REST API (Node.js)
     │
     │  Mongoose queries
     ▼
MongoDB Atlas
```

On load, the frontend sends a GET request to fetch all tasks. After any CRUD operation or drag-and-drop action, the corresponding API request is made and Redux state is updated immediately — no page refresh required.

## Running Locally

### Prerequisites

- Node.js 18+
- npm
- MongoDB (local or Atlas)
- Firebase project (only for Google login)

### 1. Clone the repository

```bash
git clone https://github.com/AarishMansur/CollEdge_Connect_Assignment.git
cd CollEdge_Connect_Assignment
```

### 2. Backend setup

```bash
cd backend
npm install
```

Create `.env` in the `backend` directory:

```env
PORT=3000
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
COOKIE_SECRET=your_cookie_signing_secret
FRONTEND_BASE_URL=http://localhost:5173
NODE_ENV=development
```

Start the backend:

```bash
npm start
```

API runs at `http://localhost:3000`.

### 3. Frontend setup

```bash
cd ../frontend
npm install
```

Create `.env` in the `frontend` directory:

```env
VITE_BACKEND_BASE_URL=http://localhost:3000
VITE_FIREBASE_API_KEY=your_firebase_api_key
```

Start the frontend:

```bash
npm run dev
```

App runs at `http://localhost:5173`.

## Environment Variables

### Backend

| Variable | Required | Purpose |
| --- | --- | --- |
| `PORT` | No | Server port, defaults to `3000` |
| `MONGODB_URI` | Yes | MongoDB connection string |
| `JWT_SECRET` | Yes | Signs and verifies JWTs |
| `COOKIE_SECRET` | Yes | Cookie Parser signing secret |
| `FRONTEND_BASE_URL` | Yes | Allowed CORS origin |
| `NODE_ENV` | No | Set to `production` on Render |

### Frontend

| Variable | Required | Purpose |
| --- | --- | --- |
| `VITE_BACKEND_BASE_URL` | Yes | Backend API base URL |
| `VITE_FIREBASE_API_KEY` | For Google login | Firebase web API key |

Only variables prefixed with `VITE_` are exposed to the browser. Never put secrets in the frontend `.env`.

## Available Scripts

### Backend
- `npm start` — starts the Express server

### Frontend
- `npm run dev` — starts the Vite dev server
- `npm run build` — builds for production
- `npm run preview` — previews the production build
- `npm run lint` — runs ESLint

## Deployment

### Backend (Render)
1. Create a Render Web Service
2. Root directory: `backend`
3. Build command: `npm install`
4. Start command: `npm start`
5. Add all backend environment variables
6. Set `NODE_ENV=production`
7. Set `FRONTEND_BASE_URL` to the Vercel frontend URL

### Frontend (Vercel)
1. Import the repository on Vercel
2. Set root directory to `frontend`
3. Build command: `npm run build`
4. Output directory: `dist`
5. Set `VITE_BACKEND_BASE_URL` to the Render backend URL
6. Add `VITE_FIREBASE_API_KEY` if Google login is enabled

## Future Improvements

- Enable authentication on task routes and associate tasks with their owner
- Add confirmation dialog before task deletion
- Add pagination for large task collections
- Add automated tests for frontend and backend
- Improve keyboard accessibility for drag and drop

## Author

**Aarish Mansur**  
GitHub: [AarishMansur](https://github.com/AarishMansur)

## License

MIT