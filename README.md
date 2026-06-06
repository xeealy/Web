# Web-Based CRM

A comprehensive Customer Relationship Management (CRM) system built with modern web technologies.

## 📋 Project Overview

This project implements a full-featured CRM application with contact management, sales pipeline tracking, activity management, and analytics.

## 🛠️ Tech Stack

### Frontend
- **Framework**: React 18+
- **State Management**: Redux Toolkit
- **UI Library**: Material-UI (MUI)
- **HTTP Client**: Axios
- **Build Tool**: Vite
- **Styling**: Tailwind CSS

### Backend
- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: PostgreSQL
- **ORM**: Sequelize or TypeORM
- **Authentication**: JWT (JSON Web Tokens)
- **API Documentation**: Swagger/OpenAPI

### DevOps & Tools
- **Version Control**: Git
- **Package Manager**: npm/yarn
- **Testing**: Jest (Backend), Vitest (Frontend)
- **Linting**: ESLint, Prettier
- **Environment**: Docker (optional)

## 📁 Project Structure

```
Web/
├── frontend/                 # React application
│   ├── src/
│   │   ├── components/      # Reusable React components
│   │   ├── pages/          # Page components
│   │   ├── store/          # Redux store
│   │   ├── services/       # API services
│   │   ├── hooks/          # Custom React hooks
│   │   ├── utils/          # Utility functions
│   │   ├── styles/         # Global styles
│   │   └── App.jsx
│   ├── public/
│   ├── package.json
│   └── vite.config.js
│
├── backend/                  # Express.js API
│   ├── src/
│   │   ├── models/         # Database models
│   │   ├── routes/         # API routes
│   │   ├── controllers/    # Route handlers
│   │   ├── middleware/     # Custom middleware
│   │   ├── services/       # Business logic
│   │   ├── config/         # Configuration files
│   │   ├── validators/     # Request validators
│   │   ├── utils/          # Utility functions
│   │   └── server.js       # Entry point
│   ├── migrations/         # Database migrations
│   ├── seeders/            # Database seeders
│   ├── tests/              # Test files
│   ├── package.json
│   └── .env.example
│
├── docs/                     # Documentation
│   ├── API.md              # API documentation
│   ├── DATABASE.md         # Database schema
│   └── SETUP.md            # Setup instructions
│
├── .gitignore
├── .env.example
└── README.md
```

## 🎯 Core Features

### 1. **Contact & Lead Management**
   - Create, read, update, delete contacts
   - Lead scoring and qualification
   - Contact segmentation
   - Bulk operations

### 2. **Sales Pipeline**
   - Opportunity tracking
   - Deal stages and progression
   - Sales forecasting
   - Win/loss analysis

### 3. **Activity & Task Management**
   - Log calls, emails, meetings
   - Task assignment and tracking
   - Activity timeline
   - Calendar integration

### 4. **Reporting & Analytics**
   - Sales performance metrics
   - Conversion funnel analysis
   - Revenue reports
   - Custom dashboards

### 5. **User Management**
   - Role-based access control (RBAC)
   - User authentication & authorization
   - Permission management
   - Activity logging

### 6. **Integration**
   - Email integration
   - Calendar sync
   - Document management
   - Third-party API connections

## 🚀 Getting Started

### Prerequisites
- Node.js 16+
- PostgreSQL 12+
- npm or yarn

### Installation

1. Clone the repository
   ```bash
   git clone https://github.com/xeealy/Web.git
   cd Web
   ```

2. Setup Backend
   ```bash
   cd backend
   cp .env.example .env
   npm install
   npm run migrate
   npm run seed
   npm run dev
   ```

3. Setup Frontend
   ```bash
   cd frontend
   npm install
   npm run dev
   ```

4. Access the application
   - Frontend: http://localhost:5173
   - Backend API: http://localhost:3000
   - API Docs: http://localhost:3000/api/docs

## 📝 API Endpoints (Base URL: /api/v1)

### Authentication
- `POST /auth/register` - Register new user
- `POST /auth/login` - User login
- `POST /auth/logout` - User logout
- `POST /auth/refresh` - Refresh token

### Contacts
- `GET /contacts` - List all contacts
- `POST /contacts` - Create new contact
- `GET /contacts/:id` - Get contact details
- `PUT /contacts/:id` - Update contact
- `DELETE /contacts/:id` - Delete contact

### Opportunities
- `GET /opportunities` - List all opportunities
- `POST /opportunities` - Create opportunity
- `GET /opportunities/:id` - Get opportunity details
- `PUT /opportunities/:id` - Update opportunity
- `DELETE /opportunities/:id` - Delete opportunity

### Activities
- `GET /activities` - List activities
- `POST /activities` - Log activity
- `GET /activities/:id` - Get activity details
- `PUT /activities/:id` - Update activity
- `DELETE /activities/:id` - Delete activity

### Reports
- `GET /reports/dashboard` - Dashboard metrics
- `GET /reports/sales` - Sales reports
- `GET /reports/activities` - Activity reports

## 🧪 Testing

```bash
# Backend tests
cd backend
npm run test
npm run test:coverage

# Frontend tests
cd frontend
npm run test
npm run test:coverage
```

## 🔧 Development

```bash
# Linting
npm run lint

# Format code
npm run format

# Build for production
npm run build
```

## 📚 Documentation

See the `docs/` folder for detailed documentation:
- [API Documentation](./docs/API.md)
- [Database Schema](./docs/DATABASE.md)
- [Setup Guide](./docs/SETUP.md)

## 🤝 Contributing

1. Create a feature branch (`git checkout -b feature/AmazingFeature`)
2. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
3. Push to the branch (`git push origin feature/AmazingFeature`)
4. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👥 Team

- **Developer**: xeealy

## 📧 Contact

For questions or feedback, please reach out via GitHub Issues.

---

**Last Updated**: 2026-06-06
