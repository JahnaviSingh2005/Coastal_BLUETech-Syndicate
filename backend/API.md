# 📡 API Documentation

Complete API reference for the Coastal Pollution Monitor backend.

## Base URL

```
http://localhost:8000
```

## Authentication

No authentication required. All endpoints are public.

---

## Endpoints

### 1. Upload Pollution Report

Upload a pollution image with location data.

**Endpoint:** `POST /api/upload`

**Content-Type:** `multipart/form-data`

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| image | File | Yes | Image file (JPEG, PNG, WebP) |
| latitude | Float | Yes | GPS latitude (-90 to 90) |
| longitude | Float | Yes | GPS longitude (-180 to 180) |
| description | String | No | Optional description |

**Example Request:**

```bash
curl -X POST "http://localhost:8000/api/upload" \
  -F "image=@pollution_photo.jpg" \
  -F "latitude=13.0827" \
  -F "longitude=80.2707" \
  -F "description=Plastic bottles found near shoreline"
```

**Success Response (200):**

```json
{
  "success": true,
  "message": "Report submitted successfully!",
  "report": {
    "id": 1,
    "image_path": "/static/uploads/abc123.jpg",
    "latitude": 13.0827,
    "longitude": 80.2707,
    "pollution_type": "plastic",
    "pollution_name": "Plastic Pollution",
    "pollution_icon": "🥤",
    "confidence": 0.85,
    "description": "Plastic bottles found near shoreline",
    "created_at": "2024-01-15T10:30:00"
  }
}
```

**Error Response (400):**

```json
{
  "detail": "Invalid file type. Allowed: image/jpeg, image/png, image/webp"
}
```

---

### 2. Get All Reports

Retrieve all pollution reports.

**Endpoint:** `GET /api/reports`

**Example Request:**

```bash
curl "http://localhost:8000/api/reports"
```

**Success Response (200):**

```json
{
  "success": true,
  "count": 5,
  "reports": [
    {
      "id": 1,
      "image_path": "abc123.jpg",
      "image_url": "/static/uploads/abc123.jpg",
      "latitude": 13.0827,
      "longitude": 80.2707,
      "pollution_type": "plastic",
      "pollution_name": "Plastic Pollution",
      "pollution_icon": "🥤",
      "pollution_color": "#ef4444",
      "confidence": 0.85,
      "description": "Plastic bottles",
      "created_at": "2024-01-15T10:30:00"
    }
  ]
}
```

---

### 3. Get Single Report

Retrieve a specific report by ID.

**Endpoint:** `GET /api/reports/{id}`

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| id | Integer | Report ID |

**Example Request:**

```bash
curl "http://localhost:8000/api/reports/1"
```

**Success Response (200):**

```json
{
  "success": true,
  "report": {
    "id": 1,
    "image_path": "abc123.jpg",
    "image_url": "/static/uploads/abc123.jpg",
    "latitude": 13.0827,
    "longitude": 80.2707,
    "pollution_type": "plastic",
    "pollution_name": "Plastic Pollution",
    "pollution_icon": "🥤",
    "pollution_color": "#ef4444",
    "pollution_description": "Plastic bottles, bags, wrappers...",
    "confidence": 0.85,
    "description": "Plastic bottles",
    "created_at": "2024-01-15T10:30:00"
  }
}
```

**Error Response (404):**

```json
{
  "detail": "Report with ID 999 not found"
}
```

---

### 4. Get Statistics

Get pollution statistics.

**Endpoint:** `GET /api/stats`

**Example Request:**

```bash
curl "http://localhost:8000/api/stats"
```

**Success Response (200):**

```json
{
  "success": true,
  "stats": {
    "total": 25,
    "by_type": {
      "plastic": 10,
      "oil_spill": 3,
      "general_waste": 8,
      "marine_debris": 4
    },
    "percentages": {
      "plastic": 40.0,
      "oil_spill": 12.0,
      "general_waste": 32.0,
      "marine_debris": 16.0
    },
    "details": [
      {
        "type": "plastic",
        "name": "Plastic Pollution",
        "icon": "🥤",
        "color": "#ef4444",
        "count": 10,
        "percentage": 40.0
      }
    ]
  }
}
```

---

### 5. Health Check

Check API health status.

**Endpoint:** `GET /api/health`

**Example Request:**

```bash
curl "http://localhost:8000/api/health"
```

**Success Response (200):**

```json
{
  "status": "healthy",
  "timestamp": "2024-01-15T10:30:00",
  "service": "Coastal Pollution Monitor API"
}
```

---

### 6. Serve Uploaded Images

Access uploaded images.

**Endpoint:** `GET /static/uploads/{filename}`

**Example:**

```
http://localhost:8000/static/uploads/abc123.jpg
```

---

## Pollution Types

| Type | Name | Color | Icon |
|------|------|-------|------|
| plastic | Plastic Pollution | #ef4444 | 🥤 |
| oil_spill | Oil Spill | #1f2937 | 🛢️ |
| general_waste | General Waste | #92400e | 🗑️ |
| marine_debris | Marine Debris | #f97316 | 🎣 |

---

## Error Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 400 | Bad Request (invalid input) |
| 404 | Not Found |
| 500 | Internal Server Error |

---

## Interactive API Docs

FastAPI provides automatic interactive documentation:

- **Swagger UI:** http://localhost:8000/docs
- **ReDoc:** http://localhost:8000/redoc
