# Local Development Setup Guide

## Database Configuration

### Option 1: SQLite (Default - No Setup Required)
The application uses SQLite by default. No additional configuration needed.

### Option 2: PostgreSQL (For Production-like Environment)

#### Step 1: Install PostgreSQL
```bash
# On Ubuntu/Debian
sudo apt-get install postgresql postgresql-contrib

# On macOS
brew install postgresql

# On Windows
# Download from https://www.postgresql.org/download/windows/
```

#### Step 2: Create Database
```bash
# Start PostgreSQL service
sudo service postgresql start  # Linux
brew services start postgresql  # macOS

# Create database and user
sudo -u postgres psql
CREATE DATABASE healthcare_assistant;
CREATE USER your_username WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE healthcare_assistant TO your_username;
\q
```

#### Step 3: Configure Environment
Edit `.env` file and uncomment/set:
```
DATABASE_URL=postgresql://your_username:your_password@localhost:5432/healthcare_assistant
```

## API Configuration

### Groq API Key Setup
1. Go to https://console.groq.com/
2. Create account or log in
3. Navigate to "API Keys" section
4. Create new API key
5. Set as environment variable (never in .env file):
```bash
export GROQ_API_KEY=your_api_key_here
```

## Running the Application

### Install Dependencies
```bash
pip install -r deployable_requirements.txt
```

### Start Application
```bash
streamlit run app.py --server.port 5000
```

## File Structure
```
healthcare-ai-assistant/
├── app.py                     # Main application
├── database.py               # Database models and operations
├── model_handler.py          # AI model integration
├── utils.py                  # Utility functions
├── components.py             # UI components
├── styles.py                 # Custom styling
├── password_validator.py     # Password validation
├── config.json              # Application configuration
├── .env                     # Environment variables
├── .gitignore               # Git ignore rules
└── deployable_requirements.txt # Dependencies
```

## Security Notes
- Never commit API keys to version control
- The .gitignore file prevents accidental exposure
- Use environment variables for sensitive data
- SQLite database file is ignored by git for security