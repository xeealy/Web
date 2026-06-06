# Database Schema

## Overview

PostgreSQL database schema for the CRM application.

## Tables

### Users
User accounts and authentication

```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  password VARCHAR(255) NOT NULL,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  role ENUM('admin', 'manager', 'user') DEFAULT 'user',
  status ENUM('active', 'inactive', 'suspended') DEFAULT 'active',
  phone VARCHAR(20),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  last_login TIMESTAMP
);
```

### Contacts
Customer and lead contact information

```sql
CREATE TABLE contacts (
  id SERIAL PRIMARY KEY,
  first_name VARCHAR(100) NOT NULL,
  last_name VARCHAR(100) NOT NULL,
  email VARCHAR(255),
  phone VARCHAR(20),
  company VARCHAR(255),
  job_title VARCHAR(100),
  status ENUM('lead', 'contact', 'customer') DEFAULT 'lead',
  source ENUM('web', 'email', 'phone', 'referral', 'other'),
  owner_id INTEGER REFERENCES users(id),
  address VARCHAR(255),
  city VARCHAR(100),
  state VARCHAR(100),
  country VARCHAR(100),
  zip_code VARCHAR(10),
  notes TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Opportunities
Sales opportunities and deals

```sql
CREATE TABLE opportunities (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  contact_id INTEGER NOT NULL REFERENCES contacts(id),
  amount DECIMAL(15, 2),
  stage ENUM('prospecting', 'negotiation', 'decision', 'closed_won', 'closed_lost') DEFAULT 'prospecting',
  probability INTEGER DEFAULT 0,
  expected_close_date DATE,
  owner_id INTEGER REFERENCES users(id),
  description TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Activities
Calls, emails, meetings, and tasks

```sql
CREATE TABLE activities (
  id SERIAL PRIMARY KEY,
  type ENUM('call', 'email', 'meeting', 'task') NOT NULL,
  title VARCHAR(255) NOT NULL,
  description TEXT,
  contact_id INTEGER REFERENCES contacts(id),
  opportunity_id INTEGER REFERENCES opportunities(id),
  owner_id INTEGER REFERENCES users(id),
  due_date DATE,
  completed_date TIMESTAMP,
  status ENUM('pending', 'in_progress', 'completed', 'cancelled') DEFAULT 'pending',
  priority ENUM('low', 'medium', 'high') DEFAULT 'medium',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Notes
General notes and comments

```sql
CREATE TABLE notes (
  id SERIAL PRIMARY KEY,
  content TEXT NOT NULL,
  contact_id INTEGER REFERENCES contacts(id),
  opportunity_id INTEGER REFERENCES opportunities(id),
  activity_id INTEGER REFERENCES activities(id),
  owner_id INTEGER NOT NULL REFERENCES users(id),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Indexes

```sql
CREATE INDEX idx_contacts_owner ON contacts(owner_id);
CREATE INDEX idx_contacts_status ON contacts(status);
CREATE INDEX idx_opportunities_owner ON opportunities(owner_id);
CREATE INDEX idx_opportunities_stage ON opportunities(stage);
CREATE INDEX idx_activities_owner ON activities(owner_id);
CREATE INDEX idx_activities_status ON activities(status);
```

## Relationships

- Users → Contacts (one-to-many): A user can own multiple contacts
- Contacts → Opportunities (one-to-many): A contact can have multiple opportunities
- Opportunities → Activities (one-to-many): An opportunity can have multiple activities
- Users → Activities (one-to-many): A user can have multiple activities
- Activities → Notes (one-to-many): An activity can have multiple notes
