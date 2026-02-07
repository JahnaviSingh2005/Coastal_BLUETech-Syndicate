# 📋 Complete Setup Guide

This guide will help you set up the Coastal Pollution Monitor from scratch.

## Prerequisites

Before starting, ensure you have:

- ✅ **Python 3.8+** - [Download](https://python.org)
- ✅ **Node.js 16+** - [Download](https://nodejs.org)
- ✅ **Git** (optional) - [Download](https://git-scm.com)

## Step 1: Project Setup

```bash
# Create project directory (if not exists)
mkdir coastal-pollution-monitor
cd coastal-pollution-monitor
```

## Step 2: Backend Setup

### 2.1 Navigate to Backend

```bash
cd backend
```

### 2.2 Create Virtual Environment

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**Mac/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### 2.3 Install Dependencies

```bash
pip install -r requirements.txt
```

### 2.4 (Optional) Enable AI Classification

For better accuracy, install CLIP:
```bash
pip install transformers torch
```

### 2.5 Start Backend Server

```bash
uvicorn main:app --reload --port 8000
```

**Expected Output:**
```
✅ Database initialized successfully!
🌊 Coastal Pollution Monitor API started!
INFO:     Uvicorn running on http://0.0.0.0:8000
```

### 2.6 Verify Backend

Open in browser: http://localhost:8000

You should see:
```json
{
  "message": "🌊 Welcome to Coastal Pollution Monitor API",
  "version": "1.0.0"
}
```

## Step 3: Frontend Setup

### 3.1 Open New Terminal

Keep backend running, open a new terminal window.

### 3.2 Navigate to Frontend

```bash
cd frontend
```

### 3.3 Install Dependencies

```bash
npm install
```

### 3.4 (Optional) Environment Configuration

Create `.env` file:
```bash
echo REACT_APP_API_URL=http://localhost:8000 > .env
```

### 3.5 Start Frontend Server

```bash
npm start
```

**Expected Output:**
```
Compiled successfully!

You can now view coastal-pollution-monitor in the browser.

  Local:            http://localhost:3000
```

## Step 4: Generate Test Data (Optional)

To populate the map with sample reports:

### 4.1 In Backend Terminal

```bash
# Make sure virtual environment is active
cd backend
python test_data.py
```

**Expected Output:**
```
🧪 Generating 10 test pollution reports...

  ✅ Report #1: plastic at Marina Beach, Chennai
  ✅ Report #2: oil_spill at Juhu Beach, Mumbai
  ...

✨ Generated 10 test reports successfully!
```

## Step 5: Test the Application

### 5.1 Full Test Flow

1. **Open Frontend**: http://localhost:3000
2. **View Home Page**: See hero section and features
3. **Go to Upload Page**: Click "Report Pollution"
4. **Upload Test Image**: Drag & drop or browse
5. **Get Location**: Click "Get My Current Location"
6. **Submit Report**: Click "Submit Report"
7. **View Results**: See classification results
8. **Check Map**: Go to Map page to see your report

### 5.2 API Testing

Test endpoints with curl:

```bash
# Get all reports
curl http://localhost:8000/api/reports

# Get statistics
curl http://localhost:8000/api/stats

# Upload a report (replace with real image path)
curl -X POST http://localhost:8000/api/upload \
  -F "image=@test_image.jpg" \
  -F "latitude=13.0827" \
  -F "longitude=80.2707" \
  -F "description=Test report"
```

## Troubleshooting

### Backend Issues

**Port already in use:**
```bash
uvicorn main:app --reload --port 8001
```

**Module not found:**
```bash
pip install -r requirements.txt
```

**Database corrupt:**
```bash
# Delete and restart - will be recreated
del pollution.db  # Windows
rm pollution.db   # Mac/Linux
```

### Frontend Issues

**npm install fails:**
```bash
# Clear cache and retry
npm cache clean --force
rm -rf node_modules
npm install
```

**Backend connection error:**
- Verify backend at http://localhost:8000
- Check CORS settings in main.py
- Ensure no firewall blocking

**Map not loading:**
- Check internet connection
- Leaflet uses OpenStreetMap tiles (requires internet)

### Location Issues

**GPS not working:**
- Allow location permission in browser
- Try manual coordinate entry
- For testing: Use coordinates like 13.0827, 80.2707 (Chennai)

## Running in Production

### Backend Production

```bash
# Without --reload for production
uvicorn main:app --host 0.0.0.0 --port 8000
```

### Frontend Production Build

```bash
npm run build
# Serve build/ folder with any static server
npx serve -s build
```

## Quick Reference

| Service | URL | Port |
|---------|-----|------|
| Backend API | http://localhost:8000 | 8000 |
| API Docs | http://localhost:8000/docs | 8000 |
| Frontend | http://localhost:3000 | 3000 |

## Need Help?

1. Check the README files in each folder
2. Review API.md for endpoint details
3. Check browser console for errors
4. Check terminal for backend errors

---

**Happy Coding! 🌊**
