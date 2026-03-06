# VitIT

> A private social platform (Reddit/Facebook-style) for VIT students.

VitIT is a lightweight campus social network for VIT students to share posts, discuss topics, and connect with classmates. This repository contains a Node/Express backend and a React + Vite frontend.

**Features**
- User signup & login (passwords hashed with `bcrypt`)
- JWT authentication with cookie-based session
- Simple protected dashboard endpoint
- Post and discussion-ready structure (extensible)

**Tech Stack**
- Backend: Node.js, Express, PostgreSQL, `bcrypt`, `jsonwebtoken`
- Frontend: React, Vite, React Router

**Repository structure**
- `backend/` — Express API and database code
  - `backend/server.js` — main server
  - `backend/src/db/createTable.js` — creates `users` table
- `frontend/` — React + Vite app

**Prerequisites**
- Node.js (v16+ recommended)
- npm or yarn
- PostgreSQL running locally (default config expects a DB named `db`)

**Environment**
Create a `.env` file in `backend/` with at least:

```
DB_PASS=your_postgres_password
JWT_SECRET=some_secure_random_string
```

**Backend setup (development)**
1. Open a terminal and change to the backend folder:

```bash
cd backend
npm install
```

2. Create the Postgres database (example using `psql`):

```bash
psql -U postgres -c "CREATE DATABASE db;"
```

3. Ensure your `DB_PASS` is set in `backend/.env`.

4. Create the `users` table (the script uses the DB configuration in `backend/src/db/db.js`):

```bash
node src/db/createTable.js
```

5. Start the server:

```bash
npm run dev
# if the `dev` script fails, run:
node server.js
```

The backend listens on port `5000` by default.

**Frontend setup (development)**
1. Change to the frontend folder and install:

```bash
cd ../frontend
npm install
npm run dev
```

The frontend runs on Vite’s default port (usually `5173`). The backend CORS is configured for `http://localhost:5173`.

**API (quick reference)**
- `POST /signup` — Register a user. Body: `{ name, email, password }`
- `POST /login` — Login. Body: `{ email, password }` — returns a cookie `jwtToken`
- `GET /dashboard` — Protected route (requires cookie), uses middleware in `backend/src/middleware/auth`

**Development notes & tips**
- Database connection is defined in `backend/src/db/db.js`. Adjust the `user`, `host`, `database`, and `port` fields if your Postgres setup differs.
- Passwords are hashed with `bcrypt` before storing.
- JWT token expiration is set to 1 hour in `backend/server.js`.
