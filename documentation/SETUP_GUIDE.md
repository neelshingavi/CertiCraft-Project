# Setup & Execution Guide

Follow these steps to run CertiCraft on a new machine.

## 1. Prerequisites
Ensure you have the following installed:
- **Node.js** (v16.0.0 or higher)
- **NPM** (v8.0.0 or higher)
- **Git**

---

## 2. Environment Configuration

### Backend Setup
1. Navigate to the `backend` folder:
   ```bash
   cd backend
   ```
2. Create a `.env` file (copy from `.env.example` if available):
   ```bash
   cp .env.example .env
   ```
3. Open `.env` and configure the following:
   - `JWT_SECRET`: Any long random string.
   - `FRONTEND_URL`: `http://localhost:5173` (for local development).
   - `MAIL_USERNAME` / `MAIL_PASSWORD`: Your Gmail credentials (use an App Password).

### Frontend Setup
Ensure the API URL in the frontend services matches your backend port (default: `http://localhost:8080/api`).

---

## 3. Installation Steps

### Step 1: Install Dependencies
Run this in both the `backend` and `frontend` directories:
```bash
# In backend directory
npm install

# In frontend directory
cd ../frontend
npm install
```

### Step 2: Initialize Database
The project uses SQLite by default for easy setup. Run migrations to create tables:
```bash
cd ../backend
npm run migrate
```
*(Note: If you are using PostgreSQL, update the .env file with your DB credentials before running this command.)*

---

## 4. Running the Application

### Option A: Standard Execution (Two Terminals)

**Terminal 1: Start Backend**
```bash
cd backend
npm run dev
```

**Terminal 2: Start Frontend**
```bash
cd frontend
npm run dev
```

### Option B: PM2 (Production/Background Mode)
If you have `pm2` installed globally, you can start both from the root:
```bash
npm run pm2:start
```

---

## 5. Accessing the App
- **Frontend**: [http://localhost:5173](http://localhost:5173)
- **Backend API**: [http://localhost:8080](http://localhost:8080)

---

## 6. Troubleshooting

- **Port Conflict**: If port 8080 is in use, kill the process:
  - Windows: `netstat -ano | findstr :8080`
  - Mac/Linux: `sudo lsof -i :8080 -t | xargs kill -9`
- **Database Errors**: Delete `database.sqlite` and re-run `npm run migrate`.
- **Email Fails**: Ensure "Less Secure App access" is off and you are using a **Google App Password**, not your regular account password.
