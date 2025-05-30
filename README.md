# AIDiary Flask App

## Production Deployment Instructions

### 1. Environment Variables
- Create a `.env` file (not committed to git) with:
  - `GOOGLE_API_KEY=your_google_api_key`
  - `SECRET_KEY=your_random_secret_key`

### 2. Build & Run with Docker
```sh
# Build the image
# (from project root)
docker build -t aidiary-flask .

# Run the container
# (make sure to mount your .env file and persist the database if needed)
docker run --env-file .env -p 8080:8080 aidiary-flask
```

### 3. Run with Gunicorn (without Docker)
```sh
# Install dependencies
pip install -r requirements.txt

# Set environment variables (on Windows PowerShell)
$env:SECRET_KEY="your_random_secret_key"
$env:GOOGLE_API_KEY="your_google_api_key"

# Run Gunicorn
python -m gunicorn app:app --bind 0.0.0.0:8080 --workers 3
```

### 4. Security & Best Practices
- Never commit `.env` or secrets to git.
- Use a strong, random `SECRET_KEY` in production.
- For scaling, use a production database (PostgreSQL/MySQL) and persistent storage for `aidiary.db`.
- Set up HTTPS and a reverse proxy (nginx) for real deployments.

### 5. Static Files
- In production, serve static files (in `/static`) via nginx or a CDN, not Flask.

### 6. Health Check
- Add a `/health` route in `app.py` for uptime monitoring if needed.

---

For more, see Flask and Gunicorn documentation.
