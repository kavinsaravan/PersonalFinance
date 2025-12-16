# Personal Finance - AI-Powered Transaction Management System

A sophisticated full-stack web application for managing personal finances with intelligent AI-powered transaction categorization and natural language insights generation. Built with React, Flask, MongoDB, and OpenAI's GPT models.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Deployment](#deployment)
- [Architecture](#architecture)
- [Contributing](#contributing)
- [License](#license)

## Overview

Personal Finance is a modern application designed to help users track and analyze their financial transactions with the power of artificial intelligence. The application leverages OpenAI's GPT-4o-mini model to automatically categorize user transactions and generate insights from natural language queries, making financial data analysis accessible and intuitive.

## Demo

https://go.screenpal.com/watch/cTlDhBnYxWb

## Features

### Core Functionality

- **Transaction Management**
  - View all transactions in an interactive data grid with sorting and pagination
  - Create new transactions manually with real-time validation
  - Upload bulk transactions via CSV files
  - Real-time filtering and search capabilities

- **AI-Powered Categorization**
  - Automatic transaction categorization using OpenAI GPT-4o-mini
  - 17 predefined categories: Office, Technology, Travel, Meals, Marketing, Utilities, Education, Entertainment, Transportation, Insurance, Professional, Rent, Security, Maintenance, Taxes, Payroll, Other
  - Intelligent merchant name analysis
  - Error detection and correction mechanisms for API responses

- **Natural Language Insights**
  - Ask questions about your finances in plain English
  - Intelligent time window extraction (e.g., "last month", "this quarter", "past 90 days")
  - AI-generated insights based on transaction patterns
  - JSON-formatted analysis for structured data consumption

- **User Authentication & Security**
  - Secure sign up and sign in with Firebase Authentication
  - Custom token-based authorization
  - Session persistence via local storage
  - Protected API endpoints with token verification
  - Email verification support

- **Modern User Interface**
  - Responsive Material-UI design
  - Intuitive authentication screens
  - Tabbed interface for easy navigation (Transactions and Insights)
  - Advanced data grid with customizable columns
  - User profile management with dropdown menu

## Tech Stack

### Frontend

| Technology | Version | Purpose |
|------------|---------|---------|
| React | 19.1.0 | Core UI framework |
| Material-UI (MUI) | 7.2.0 | Component library and design system |
| @mui/x-data-grid | 8.8.0 | Advanced data grid for transactions |
| @mui/icons-material | 7.2.0 | Icon library |
| @emotion/react | 11.14.0 | CSS-in-JS styling |
| @emotion/styled | 11.14.1 | Styled components |
| Firebase SDK | Latest | Authentication |
| React Scripts | 5.0.1 | Build tooling |
| Testing Library | Latest | Unit and integration testing |

### Backend

| Technology | Version | Purpose |
|------------|---------|---------|
| Flask | 2.3.2 | Web framework |
| FastAPI | 0.115.12 | Alternative API framework |
| OpenAI API | 1.0.0+ | AI/ML integration (GPT-4o-mini) |
| PyMongo | 4.4.1 | MongoDB driver |
| Firebase Admin SDK | 7.0.0 | Authentication verification |
| Pydantic | 2.11.3 | Data validation |
| flask-cors | 4.0.0 | CORS support |
| python-dotenv | 1.0.0 | Environment management |
| pandas | Latest | Data manipulation |
| requests | 2.32.3 | HTTP client |

### Database & Authentication

- **Database**: MongoDB (NoSQL document database)
- **Authentication**: Firebase (Google's authentication platform)
- **Hosting**: Render (both frontend and backend)

## Project Structure

```
PersonalFinance/
├── pf-reactjs/                    # React frontend application
│   ├── public/                    # Static assets
│   │   ├── index.html
│   │   ├── manifest.json
│   │   ├── favicon.ico
│   │   └── logos (192x192, 512x512)
│   ├── src/                       # React source code
│   │   ├── App.js                 # Main app component with tab navigation
│   │   ├── App.css                # Global styles
│   │   ├── theme.js               # Material-UI theme customization
│   │   ├── AuthContext.js         # Auth state management (Context API)
│   │   ├── AuthScreen.js          # Auth wrapper component
│   │   ├── SignIn.js              # Sign in form
│   │   ├── SignUp.js              # Sign up form
│   │   ├── AppBar.js              # Navigation bar with user menu
│   │   ├── TransactionTable.js    # Main transactions view with DataGrid
│   │   ├── InsightsPanel.js       # AI-powered insights query interface
│   │   ├── firebaseConfig.js      # Firebase SDK initialization
│   │   ├── api.js                 # API utility functions
│   │   ├── index.js               # React DOM render entry point
│   │   ├── reportWebVitals.js     # Performance metrics
│   │   ├── setupTests.js          # Test configuration
│   │   └── index.css              # Base styles
│   ├── build/                     # Production build output
│   ├── node_modules/              # npm dependencies
│   ├── package.json               # npm configuration
│   ├── .env                       # Environment variables
│   └── README.md                  # Frontend documentation
│
└── pf-api-server/                 # Python Flask backend
    ├── app.py                     # Main Flask application (804 lines)
    ├── firebase_auth.py           # Firebase authentication helper
    ├── mongo.py                   # MongoDB connection example
    ├── requirements.txt           # Python dependencies
    ├── .flaskenv                  # Flask environment config
    ├── Procfile                   # Render deployment config
    ├── Tools/                     # Utility scripts
    │   ├── csvfileimport.py       # CSV import tool
    │   └── xmlfileimport.py       # XML import tool
    ├── app.log                    # Application logs
    ├── openai_api.log             # OpenAI API call logs
    ├── api_errors.log             # Error tracking logs
    ├── sample_sales_data.csv      # Sample data
    └── myenv/                     # Python virtual environment
```

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v14.0.0 or higher)
- **npm** (v6.0.0 or higher)
- **Python** (v3.8 or higher)
- **pip** (Python package manager)
- **MongoDB** (v4.0 or higher) - Local or cloud instance
- **Firebase Account** - For authentication services
- **OpenAI API Key** - For AI-powered features

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/PersonalFinance.git
cd PersonalFinance
```

### 2. Frontend Setup

```bash
cd pf-reactjs
npm install
```

### 3. Backend Setup

```bash
cd ../pf-api-server

# Create and activate virtual environment
python -m venv myenv

# On macOS/Linux:
source myenv/bin/activate

# On Windows:
myenv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

## Configuration

### Frontend Configuration

Create a `.env` file in the `pf-reactjs` directory:

```env
REACT_APP_API_URL=http://localhost:5000
```

Update `src/firebaseConfig.js` with your Firebase project credentials:

```javascript
const firebaseConfig = {
  apiKey: "your-api-key",
  authDomain: "your-auth-domain",
  projectId: "your-project-id",
  storageBucket: "your-storage-bucket",
  messagingSenderId: "your-messaging-sender-id",
  appId: "your-app-id"
};
```

### Backend Configuration

Create a `pf.env` file in the `pf-api-server` directory:

```env
# OpenAI Configuration
OPENAI_API_KEY=sk-your-openai-api-key-here

# MongoDB Configuration
MONGO_HOST=localhost
MONGO_PORT=27017
MONGO_DB_NAME=finance_db
MONGO_DB_USERNAME=your_username
MONGO_DB_PASSWORD=your_password

# Firebase Admin SDK
FIREBASE_CREDENTIALS_JSON={"type": "service_account", "project_id": "...", ...}

# Server Configuration
PF_SERVER_PORT=5000
```

### Firebase Admin SDK Setup

1. Go to Firebase Console > Project Settings > Service Accounts
2. Generate a new private key (downloads JSON file)
3. Copy the entire JSON content into the `FIREBASE_CREDENTIALS_JSON` environment variable

### MongoDB Setup

If running MongoDB locally:

```bash
# Start MongoDB
mongod --dbpath /path/to/data/directory

# Or use MongoDB Atlas for cloud-hosted database
# Update MONGO_HOST with Atlas connection string
```

## Running the Application

### Development Mode

#### 1. Start the Backend Server

```bash
cd pf-api-server
source myenv/bin/activate  # On Windows: myenv\Scripts\activate
python app.py
```

The Flask server will start on `http://localhost:5000`

#### 2. Start the Frontend Development Server

```bash
cd pf-reactjs
npm start
```

The React app will open in your browser at `http://localhost:3000`

### Production Build

#### Build Frontend

```bash
cd pf-reactjs
npm run build
```

This creates an optimized production bundle in the `build/` directory.

#### Run Tests

```bash
# Frontend tests
cd pf-reactjs
npm test

# Backend tests (if available)
cd pf-api-server
pytest
```

## API Documentation

### Base URL

- Development: `http://localhost:5000`
- Production: `https://your-api-url.onrender.com`

### Authentication Endpoints

#### POST `/api/signup`

Register a new user.

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securepassword"
}
```

**Response:**
```json
{
  "message": "User created successfully",
  "customToken": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...",
  "idToken": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjE...",
  "userId": "abc123xyz"
}
```

#### POST `/api/signin`

Authenticate an existing user.

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securepassword"
}
```

**Response:**
```json
{
  "message": "Sign-in successful",
  "idToken": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjE...",
  "userId": "abc123xyz"
}
```

#### GET `/api/profile`

Get authenticated user profile.

**Headers:**
```
Authorization: Bearer <idToken>
```

**Response:**
```json
{
  "uid": "abc123xyz",
  "email": "user@example.com",
  "emailVerified": false,
  "displayName": null
}
```

### Transaction Endpoints

#### GET `/api/entries`

Fetch all transactions for the authenticated user.

**Headers:**
```
Authorization: Bearer <idToken>
```

**Response:**
```json
[
  {
    "_id": "507f1f77bcf86cd799439011",
    "date": "2024-01-15",
    "merchant": "Amazon",
    "amount": 49.99,
    "category": "Technology",
    "userId": "abc123xyz"
  }
]
```

#### POST `/api/entries`

Create a new transaction.

**Headers:**
```
Authorization: Bearer <idToken>
```

**Request Body:**
```json
{
  "date": "2024-01-15",
  "merchant": "Starbucks",
  "amount": 5.50
}
```

**Response:**
```json
{
  "message": "Entry added successfully",
  "id": "507f1f77bcf86cd799439012"
}
```

#### POST `/api/categorize`

Get AI-powered category suggestion for a merchant.

**Headers:**
```
Authorization: Bearer <idToken>
```

**Request Body:**
```json
{
  "merchant": "Starbucks"
}
```

**Response:**
```json
{
  "category": "Meals"
}
```

#### POST `/api/uploadcsv`

Bulk upload transactions via CSV.

**Headers:**
```
Authorization: Bearer <idToken>
```

**Request Body:**
```json
{
  "data": [
    {
      "date": "2024-01-15",
      "merchant": "Target",
      "amount": 78.45
    },
    {
      "date": "2024-01-16",
      "merchant": "Shell Gas",
      "amount": 42.00
    }
  ]
}
```

**Response:**
```json
{
  "message": "Bulk upload successful",
  "inserted_ids": ["507f...", "508f..."],
  "count": 2
}
```

### Insights Endpoints

#### GET `/api/insights`

Generate AI-powered insights from natural language query.

**Headers:**
```
Authorization: Bearer <idToken>
```

**Query Parameters:**
- `query` (required): Natural language question about finances

**Example Request:**
```
GET /api/insights?query=What%20did%20I%20spend%20on%20food%20last%20month?
```

**Response:**
```json
{
  "insights": {
    "total_spent": 345.67,
    "transaction_count": 23,
    "average_transaction": 15.03,
    "top_merchants": ["Starbucks", "Chipotle", "Whole Foods"],
    "summary": "You spent $345.67 on food last month across 23 transactions..."
  }
}
```

### Logging Endpoints

#### GET `/api/logs/errors`

View error logs (requires authentication).

#### GET `/api/logs/openai`

View OpenAI API call logs (requires authentication).

### Response Codes

- `200` - Success
- `201` - Created
- `400` - Bad Request (validation error)
- `401` - Unauthorized (missing or invalid token)
- `404` - Not Found
- `500` - Internal Server Error

## Deployment

### Render Deployment (Recommended)

Both the frontend and backend are configured for deployment on Render.

#### Backend Deployment

1. Connect your GitHub repository to Render
2. Create a new Web Service
3. Configure environment variables (from `pf.env`)
4. Build Command: `pip install -r requirements.txt`
5. Start Command: `python app.py` (defined in Procfile)

#### Frontend Deployment

1. Create a new Static Site on Render
2. Build Command: `npm install && npm run build`
3. Publish Directory: `build`
4. Set environment variable: `REACT_APP_API_URL=https://your-backend-url.onrender.com`

## Architecture

### System Architecture

```
┌─────────────────┐         ┌─────────────────┐         ┌─────────────────┐
│                 │         │                 │         │                 │
│  React Frontend │◄────────┤  Flask Backend  │◄────────┤   MongoDB       │
│  (Port 3000)    │  REST   │  (Port 5000)    │         │   Database      │
│                 │   API   │                 │         │                 │
└────────┬────────┘         └────────┬────────┘         └─────────────────┘
         │                           │
         │                           │
         ▼                           ▼
┌─────────────────┐         ┌─────────────────┐
│                 │         │                 │
│  Firebase Auth  │         │  OpenAI API     │
│                 │         │  (GPT-4o-mini)  │
│                 │         │                 │
└─────────────────┘         └─────────────────┘
```

### Data Flow

1. **Authentication Flow**
   - User signs up/in through React frontend
   - Backend creates Firebase user and issues custom tokens
   - Client stores token in localStorage
   - All API requests include token in Authorization header
   - Backend verifies token before processing requests

2. **Transaction Categorization Flow**
   - User creates transaction with merchant name
   - Frontend sends merchant name to `/api/categorize`
   - Backend calls OpenAI API with GPT-4o-mini
   - AI returns suggested category from predefined list
   - Category is returned to frontend for user confirmation
   - Transaction is saved to MongoDB with category

3. **Insights Generation Flow** (3-step process)
   - User enters natural language query in Insights panel
   - Backend extracts time window from query using AI
   - MongoDB queries transactions within date range
   - AI analyzes matching transactions and generates insights
   - Insights returned as structured JSON

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request



