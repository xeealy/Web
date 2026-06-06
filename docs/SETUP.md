# Setup Guide

## Prerequisites

- Node.js 16.x or higher
- PostgreSQL 12.x or higher
- npm 7.x or yarn 1.22.x
- Git

## Backend Setup

### 1. Database Setup

```bash
# Create PostgreSQL database and user
sudo -u postgres psql

# In PostgreSQL CLI:
CREATE USER crm_user WITH PASSWORD 'your_secure_password';
CREATE DATABASE crm_db OWNER crm_user;
ALTER ROLE crm_user SET client_encoding TO 'utf8';
ALTER ROLE crm_user SET default_transaction_isolation TO 'read committed';
ALTER ROLE crm_user SET default_transaction_deferrable TO on;
GRANT ALL PRIVILEGES ON DATABASE crm_db TO crm_user;
\q
```

### 2. Backend Installation

```bash
cd backend
cp .env.example .env
```

Update `.env` with your database credentials:

```env
DB_HOST=localhost
DB_PORT=5432
DB_NAME=crm_db
DB_USER=crm_user
DB_PASSWORD=your_secure_password_here
```

```bash
npm install
npm run migrate
npm run seed
npm run dev
```

Backend will run on http://localhost:3000

## Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

Frontend will run on http://localhost:5173

## Docker Setup (Optional)

```bash
docker-compose up -d
```

This will start:
- PostgreSQL on port 5432
- Backend API on port 3000
- Frontend on port 5173

## Verification

1. Check Backend: `curl http://localhost:3000/api/v1/health`
2. Check Frontend: Open http://localhost:5173 in browser
3. API Docs: http://localhost:3000/api/docs

## Troubleshooting

### Port already in use
```bash
# Find process using port 3000
lsof -i :3000
# Kill process
kill -9 <PID>
```

### Database connection error
- Verify PostgreSQL is running
- Check .env credentials
- Ensure database user has proper permissions

### Node modules issues
```bash
rm -rf node_modules package-lock.json
npm install
```
