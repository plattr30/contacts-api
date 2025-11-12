# Contacts REST API

A FastAPI-based REST API for managing contacts with PostgreSQL database.

## Features

- ✅ Full CRUD operations (Create, Read, Update, Delete)
- ✅ PostgreSQL database integration
- ✅ Automatic API documentation (Swagger UI)
- ✅ Data validation with Pydantic
- ✅ Email validation
- ✅ Timestamps (created_at, updated_at)
- ✅ Ready for Railway deployment

## API Endpoints

### Base URL
- `GET /` - Welcome message and API info

### Contacts
- `POST /contacts/` - Create a new contact
- `GET /contacts/` - Get all contacts (with pagination)
- `GET /contacts/{contact_id}` - Get a specific contact
- `PUT /contacts/{contact_id}` - Update a contact
- `DELETE /contacts/{contact_id}` - Delete a contact

## Contact Schema

```json
{
  "first_name": "string",
  "last_name": "string",
  "email": "user@example.com",
  "phone": "string (optional)",
  "company": "string (optional)",
  "notes": "string (optional)"
}
```

## Local Development

### Prerequisites
- Python 3.8+
- pip

### Setup

1. Clone the repository:
```bash
git clone <your-repo-url>
cd contacts-api
```

2. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Run the application:
```bash
uvicorn main:app --reload
```

5. Open your browser and visit:
   - API: http://localhost:8000
   - Swagger docs: http://localhost:8000/docs
   - ReDoc: http://localhost:8000/redoc

## Deploy to Railway

### Step 1: Push to GitHub

1. Initialize git (if not already done):
```bash
git init
git add .
git commit -m "Initial commit - Contacts API"
```

2. Create a new repository on GitHub

3. Push your code:
```bash
git remote add origin https://github.com/yourusername/contacts-api.git
git branch -M main
git push -u origin main
```

### Step 2: Deploy on Railway

1. Go to [railway.app](https://railway.app) and sign in with GitHub

2. Click **"New Project"**

3. Select **"Deploy from GitHub repo"**

4. Choose your `contacts-api` repository

5. Railway will automatically detect it's a Python project and start deploying

### Step 3: Add PostgreSQL Database

1. In your Railway project, click **"New"** → **"Database"** → **"Add PostgreSQL"**

2. Railway will automatically:
   - Create a PostgreSQL database
   - Set the `DATABASE_URL` environment variable
   - Connect it to your application

3. Your app will automatically restart and connect to the database

### Step 4: Access Your API

1. Click on your FastAPI service in Railway

2. Go to **"Settings"** → **"Networking"** → **"Generate Domain"**

3. Railway will give you a public URL like: `https://your-app.railway.app`

4. Visit your API:
   - API: `https://your-app.railway.app`
   - Swagger docs: `https://your-app.railway.app/docs`

## Testing the API

### Using Swagger UI (Easiest)
1. Go to `/docs` on your deployed URL
2. Use the interactive interface to test all endpoints

### Using cURL

Create a contact:
```bash
curl -X POST "https://your-app.railway.app/contacts/" \
  -H "Content-Type: application/json" \
  -d '{
    "first_name": "John",
    "last_name": "Doe",
    "email": "john.doe@example.com",
    "phone": "+1234567890",
    "company": "Acme Corp"
  }'
```

Get all contacts:
```bash
curl "https://your-app.railway.app/contacts/"
```

Get a specific contact:
```bash
curl "https://your-app.railway.app/contacts/1"
```

Update a contact:
```bash
curl -X PUT "https://your-app.railway.app/contacts/1" \
  -H "Content-Type: application/json" \
  -d '{
    "phone": "+9876543210"
  }'
```

Delete a contact:
```bash
curl -X DELETE "https://your-app.railway.app/contacts/1"
```

## Project Structure

```
contacts-api/
├── main.py           # FastAPI application and routes
├── models.py         # SQLAlchemy database models
├── schemas.py        # Pydantic schemas for validation
├── database.py       # Database configuration
├── requirements.txt  # Python dependencies
├── Procfile         # Railway start command
├── .gitignore       # Git ignore rules
└── README.md        # This file
```

## Environment Variables

The app automatically uses Railway's `DATABASE_URL` environment variable. For local development without PostgreSQL, it falls back to SQLite.

## Free Tier Limits

Railway provides $5 free credit per month, which includes:
- Your FastAPI application
- PostgreSQL database
- Public domain

This is plenty for development and small projects!

## Troubleshooting

### Database connection issues
- Make sure the PostgreSQL service is running in Railway
- Check that the `DATABASE_URL` variable is set
- Railway automatically manages this, so you shouldn't need to do anything

### Deployment fails
- Check the logs in Railway dashboard
- Ensure all files are committed to Git
- Verify `requirements.txt` has all dependencies

### App doesn't start
- Check that `Procfile` exists and is correct
- Verify the Railway logs for error messages

## Next Steps

- Add authentication (JWT tokens)
- Add search/filter functionality
- Add pagination improvements
- Add rate limiting
- Add tests (pytest)
- Add Docker support

## License

MIT
