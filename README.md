# Personal Finance Tracker

A full-stack AI-powered personal finance management application that helps users track expenses, categorize transactions, and gain intelligent insights into their spending habits through natural language queries.

## Summary

Personal Finance Tracker is a modern web application that combines transaction management with artificial intelligence to provide users with a comprehensive view of their financial activities. The application features secure user authentication, intuitive transaction management, AI-powered automatic categorization, and a natural language insights engine that allows users to query their financial data conversationally.

## Features

### Authentication & Security
- **User Registration & Sign-in**: Secure authentication powered by Firebase
- **Protected Routes**: Token-based authorization for API endpoints
- **Session Management**: Persistent user sessions with automatic token refresh

### Transaction Management
- **Transaction CRUD Operations**: Create, read, update, and delete financial transactions
- **Data Grid Interface**: Interactive table with sorting, filtering, and pagination
- **Bulk CSV Upload**: Import multiple transactions from CSV files
- **Transaction Fields**: Date, merchant, category, amount tracking
- **Real-time Updates**: Instant reflection of changes in the UI

### AI-Powered Features
- **Smart Categorization**: Automatic transaction categorization using OpenAI GPT-4o-mini
  - Intelligent merchant recognition
  - 17+ predefined spending categories
  - Error detection and validation
- **Natural Language Insights**: Query your finances using everyday language
  - Examples: "How much did I spend on groceries this month?"
  - Automatic time period extraction
  - AI-generated financial analysis and recommendations
  - Visual presentation of insights

### Data Visualization & Analysis
- **Transaction Overview**: Comprehensive view of all financial activities
- **Category Breakdown**: Spending analysis by category
- **Time-based Filtering**: Query transactions by custom date ranges
- **Search & Sort**: Find specific transactions quickly

### Monitoring & Logging
- **Comprehensive Logging**: Application, API, and error logging
- **API Call Tracking**: Monitor OpenAI API usage and performance
- **Error Detection**: Automatic logging of categorization mistakes
- **Debug Endpoints**: View logs through dedicated API endpoints

## Technology Stack

### Frontend
- **React.js** (v19.1.0) - UI framework
- **Material-UI** (v7.2.0) - Component library
  - @mui/material - Core components
  - @mui/icons-material - Icon set
  - @mui/x-data-grid - Advanced data table
- **Emotion** - CSS-in-JS styling
- **Firebase SDK** - Client-side authentication
- **React Scripts** (v5.0.1) - Build tooling

### Backend
- **Python** (3.x) - Server runtime
- **Flask** (v2.3.2) - Web framework
- **Flask-CORS** (v4.0.0) - Cross-origin resource sharing
- **PyMongo** (v4.4.1) - MongoDB driver
- **Firebase Admin SDK** (v7.0.0) - Server-side authentication
- **OpenAI SDK** (v1.0.0+) - AI integration
- **Pydantic** (v2.11.3) - Data validation
- **Python-dotenv** (v1.0.0) - Environment configuration

### Database
- **MongoDB** - NoSQL database for transaction storage
  - Document-based storage
  - SCRAM-SHA-1 authentication
  - Configurable connection parameters

### External APIs & Services
- **Firebase Authentication** - User management and authentication
- **OpenAI API** (GPT-4o-mini) - AI-powered features
  - Transaction categorization
  - Financial insights generation
  - Natural language processing
- **MongoDB Atlas** (optional) - Cloud database hosting

### Development Tools
- **ESLint** - JavaScript linting
- **Jest** - Testing framework
- **Babel** - JavaScript transpilation
- **Dotenv** - Environment variable management

## Project Structure

```
PersonalFinance/
├── Client/
│   └── pf-reactjs/          # React frontend application
│       ├── src/
│       │   ├── App.js               # Main application component
│       │   ├── AuthContext.js       # Authentication context provider
│       │   ├── AuthComponent.js     # Authentication UI
│       │   ├── TransactionTable.js  # Transaction management
│       │   ├── InsightsPanel.js     # AI insights interface
│       │   ├── AppBar.js            # Navigation bar
│       │   ├── api.js               # API utility functions
│       │   └── firebaseConfig.js    # Firebase configuration
│       └── package.json
│
└── Server/
    └── pf-api-server/       # Flask backend server
        ├── app.py                   # Main Flask application
        ├── firebase_auth.py         # Firebase authentication logic
        ├── requirements.txt         # Python dependencies
        ├── app.env                  # Environment variables (not in repo)
        └── Tools/                   # Utility scripts
```

## Prerequisites

Before running this application, ensure you have:

- **Node.js** (v14.x or higher) and npm
- **Python** (v3.8 or higher)
- **MongoDB** instance (local or cloud)
- **Firebase Project** with Authentication enabled
- **OpenAI API Key** with access to GPT-4o-mini

## Installation & Setup

### 1. Clone the Repository

```bash
git clone <repository-url>
cd PersonalFinance
```

### 2. Backend Setup

#### Install Python Dependencies

```bash
cd Server/pf-api-server
pip install -r requirements.txt
```

#### Configure Environment Variables

Create an `app.env` file in the `Server` directory:

```env
# OpenAI Configuration
OPENAI_API_KEY=your_openai_api_key_here

# MongoDB Configuration
MONGO_HOST=localhost
MONGO_PORT=27017
MONGO_DB_NAME=your_database_name
MONGO_DB_USERNAME=your_username
MONGO_DB_PASSWORD=your_password

# Firebase Configuration (JSON string)
FIREBASE_CREDENTIALS_JSON={"type":"service_account","project_id":"..."}

# Server Configuration
PF_SERVER_PORT=5000
```

#### Set Up Firebase Admin

1. Go to Firebase Console > Project Settings > Service Accounts
2. Generate a new private key (JSON file)
3. Convert the JSON content to a string and add to `FIREBASE_CREDENTIALS_JSON` in `app.env`

### 3. Frontend Setup

#### Install Node Dependencies

```bash
cd Client/pf-reactjs
npm install
```

#### Configure Environment Variables

Create a `.env` file in the `Client/pf-reactjs` directory:

```env
REACT_APP_API_URL=http://localhost:5000

# Firebase Web Configuration
REACT_APP_FIREBASE_API_KEY=your_firebase_api_key
REACT_APP_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
REACT_APP_FIREBASE_PROJECT_ID=your_project_id
REACT_APP_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
REACT_APP_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
REACT_APP_FIREBASE_APP_ID=your_app_id
```

#### Set Up Firebase Client Configuration

Update `src/firebaseConfig.js` with your Firebase web app configuration.

## How to Start the Application

### Start the Backend Server

```bash
cd Server/pf-api-server
python app.py
```

The Flask server will start on `http://localhost:5000` (or the port specified in `PF_SERVER_PORT`)

### Start the Frontend Application

In a new terminal:

```bash
cd Client/pf-reactjs
npm start
```

The React app will start on `http://localhost:3000` and automatically open in your browser.

## API Endpoints

### Authentication
- `POST /api/signup` - Create new user account
- `POST /api/signin` - Sign in existing user
- `GET /api/profile` - Get user profile (requires authentication)

### Transactions
- `GET /api/entries` - Retrieve all transactions
- `POST /api/entries` - Create new transaction
- `POST /api/uploadcsv` - Bulk upload transactions from CSV
- `POST /api/check_transaction` - Validate transaction data

### AI Features
- `POST /api/categorize` - Categorize transaction using AI
- `GET /api/insights` - Get AI-generated financial insights

### Monitoring
- `GET /api/logs/errors` - View error logs
- `GET /api/logs/openai` - View OpenAI API call logs

## Usage Examples

### Adding a Transaction

1. Navigate to the Transactions tab
2. Click "Add Transaction"
3. Fill in date, merchant, category, and amount
4. Click "Save"

### AI Categorization

1. View any transaction with "Uncategorized" status
2. Click the "Categorize" button
3. AI will suggest the most appropriate category
4. Accept or modify the suggestion

### Getting Financial Insights

1. Navigate to the Insights tab
2. Enter a natural language query, such as:
   - "What did I spend on dining last month?"
   - "Show my top spending categories this week"
   - "How much have I spent on technology?"
3. Click "Get Insights"
4. View AI-generated analysis and recommendations

### CSV Upload

1. Prepare a CSV file with columns: date, merchant, amount, category (optional)
2. Click the upload icon in the Transactions table
3. Select your CSV file
4. Transactions will be imported and appear in the table

## Configuration

### Transaction Categories

The following categories are available:
- Office
- Technology
- Travel
- Meals
- Marketing
- Utilities
- Education
- Entertainment
- Transportation
- Insurance
- Professional
- Rent
- Security
- Maintenance
- Taxes
- Payroll
- Other

Categories can be customized in `Server/pf-api-server/app.py` (line 318-324)

### OpenAI Model Configuration

The application uses GPT-4o-mini by default. To change the model, update the `model` parameter in:
- `app.py` line 333 (categorization)
- `app.py` line 464 (time window extraction)
- `app.py` line 542 (insights generation)

## Deployment

### Backend Deployment

The Flask application can be deployed to:
- Heroku (Procfile included)
- AWS EC2/Elastic Beanstalk
- Google Cloud Run
- DigitalOcean App Platform

**Environment Variables**: Ensure all environment variables from `app.env` are configured in your hosting platform.

### Frontend Deployment

The React app can be deployed to:
- Vercel
- Netlify
- Render
- GitHub Pages

**Build Command**: `npm run build`
**Environment Variables**: Set `REACT_APP_API_URL` to your production backend URL.

### Production Considerations

1. **Security**:
   - Use HTTPS for all communications
   - Rotate API keys regularly
   - Implement rate limiting
   - Enable CORS only for trusted domains

2. **Database**:
   - Use MongoDB Atlas for production
   - Enable authentication and encryption
   - Set up regular backups

3. **Monitoring**:
   - Set up error tracking (e.g., Sentry)
   - Monitor API usage and costs
   - Configure log rotation

## Development

### Running Tests

**Frontend**:
```bash
cd Client/pf-reactjs
npm test
```

**Backend**:
```bash
cd Server/pf-api-server
python -m pytest
```

### Code Style

- Frontend follows ESLint React configuration
- Backend follows PEP 8 Python style guide

## Troubleshooting

### Common Issues

**Backend won't start**:
- Verify all environment variables are set correctly
- Check MongoDB connection parameters
- Ensure Python dependencies are installed

**Frontend can't connect to backend**:
- Verify `REACT_APP_API_URL` is correct
- Check CORS settings in `app.py`
- Ensure backend server is running

**Authentication fails**:
- Verify Firebase configuration
- Check Firebase credentials JSON
- Ensure Firebase Authentication is enabled in console

**AI features not working**:
- Verify OpenAI API key is valid
- Check API quota and billing
- Review error logs at `/api/logs/errors`

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes with clear commit messages
4. Test thoroughly
5. Submit a pull request

## License

This project is licensed under the MIT License.

## Support

For issues, questions, or contributions, please open an issue in the GitHub repository.

## Acknowledgments

- Firebase for authentication services
- OpenAI for AI capabilities
- Material-UI for React components
- MongoDB for database solutions

---

**Built with React, Flask, MongoDB, and AI**

