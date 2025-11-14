# API Documentation

## Overview

This document outlines the planned API integration for the Migraine Tracker application. Currently, the app uses mock data, but this documentation serves as a blueprint for future backend integration.

## Table of Contents

- [API Base URL](#api-base-url)
- [Authentication](#authentication)
- [Endpoints](#endpoints)
  - [User Management](#user-management)
  - [Migraine Episodes](#migraine-episodes)
  - [Predictions](#predictions)
  - [Statistics](#statistics)
  - [Settings](#settings)
- [Data Models](#data-models)
- [Error Handling](#error-handling)
- [Rate Limiting](#rate-limiting)
- [Versioning](#versioning)

## API Base URL

```
Production: https://api.migrainetracker.app/v1
Development: https://dev-api.migrainetracker.app/v1
Local: http://localhost:3000/v1
```

## Authentication

### Authentication Flow

The API will use JWT (JSON Web Tokens) for authentication:

```
1. User Login → POST /auth/login
2. Receive JWT Token
3. Include token in subsequent requests:
   Authorization: Bearer <token>
```

### Auth Endpoints

#### Register User

```http
POST /auth/register
```

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123",
  "firstName": "John",
  "lastName": "Doe"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "userId": "user_123",
    "email": "user@example.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "refresh_token_here"
  }
}
```

#### Login

```http
POST /auth/login
```

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "userId": "user_123",
    "email": "user@example.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "refresh_token_here",
    "expiresIn": 3600
  }
}
```

#### Refresh Token

```http
POST /auth/refresh
```

**Request Body:**
```json
{
  "refreshToken": "refresh_token_here"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "token": "new_jwt_token",
    "expiresIn": 3600
  }
}
```

## Endpoints

### User Management

#### Get User Profile

```http
GET /users/profile
Authorization: Bearer <token>
```

**Response:**
```json
{
  "success": true,
  "data": {
    "userId": "user_123",
    "email": "user@example.com",
    "firstName": "John",
    "lastName": "Doe",
    "createdAt": "2024-01-15T10:30:00Z",
    "preferences": {
      "notifications": true,
      "reminders": false,
      "analytics": true
    }
  }
}
```

#### Update User Profile

```http
PATCH /users/profile
Authorization: Bearer <token>
```

**Request Body:**
```json
{
  "firstName": "Jane",
  "lastName": "Smith"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "userId": "user_123",
    "email": "user@example.com",
    "firstName": "Jane",
    "lastName": "Smith",
    "updatedAt": "2024-01-20T14:30:00Z"
  }
}
```

### Migraine Episodes

#### Get All Episodes

```http
GET /episodes
Authorization: Bearer <token>

Query Parameters:
- limit: Number (default: 20, max: 100)
- offset: Number (default: 0)
- startDate: ISO 8601 date
- endDate: ISO 8601 date
- sortBy: 'date' | 'intensity' (default: 'date')
- order: 'asc' | 'desc' (default: 'desc')
```

**Response:**
```json
{
  "success": true,
  "data": {
    "episodes": [
      {
        "id": "episode_456",
        "userId": "user_123",
        "date": "2024-01-20T15:30:00Z",
        "intensity": 7,
        "duration": 480,
        "triggers": ["Stress", "Sleep"],
        "symptoms": ["Nausea", "Sensitivity to Light"],
        "notes": "Started after work meeting",
        "createdAt": "2024-01-20T15:35:00Z",
        "updatedAt": "2024-01-20T15:35:00Z"
      }
    ],
    "pagination": {
      "total": 45,
      "limit": 20,
      "offset": 0,
      "hasMore": true
    }
  }
}
```

#### Get Single Episode

```http
GET /episodes/:episodeId
Authorization: Bearer <token>
```

**Response:**
```json
{
  "success": true,
  "data": {
    "id": "episode_456",
    "userId": "user_123",
    "date": "2024-01-20T15:30:00Z",
    "intensity": 7,
    "duration": 480,
    "triggers": ["Stress", "Sleep"],
    "symptoms": ["Nausea", "Sensitivity to Light"],
    "notes": "Started after work meeting",
    "createdAt": "2024-01-20T15:35:00Z",
    "updatedAt": "2024-01-20T15:35:00Z"
  }
}
```

#### Create Episode

```http
POST /episodes
Authorization: Bearer <token>
```

**Request Body:**
```json
{
  "date": "2024-01-20T15:30:00Z",
  "intensity": 7,
  "duration": 480,
  "triggers": ["Stress", "Sleep"],
  "symptoms": ["Nausea", "Sensitivity to Light"],
  "notes": "Started after work meeting"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "id": "episode_456",
    "userId": "user_123",
    "date": "2024-01-20T15:30:00Z",
    "intensity": 7,
    "duration": 480,
    "triggers": ["Stress", "Sleep"],
    "symptoms": ["Nausea", "Sensitivity to Light"],
    "notes": "Started after work meeting",
    "createdAt": "2024-01-20T15:35:00Z"
  }
}
```

#### Update Episode

```http
PATCH /episodes/:episodeId
Authorization: Bearer <token>
```

**Request Body:**
```json
{
  "intensity": 8,
  "duration": 540,
  "notes": "Intensity increased in the evening"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "id": "episode_456",
    "userId": "user_123",
    "intensity": 8,
    "duration": 540,
    "notes": "Intensity increased in the evening",
    "updatedAt": "2024-01-20T18:00:00Z"
  }
}
```

#### Delete Episode

```http
DELETE /episodes/:episodeId
Authorization: Bearer <token>
```

**Response:**
```json
{
  "success": true,
  "message": "Episode deleted successfully"
}
```

### Predictions

#### Get Predictions

```http
GET /predictions
Authorization: Bearer <token>

Query Parameters:
- days: Number (default: 7, max: 30) - Number of days to predict
```

**Response:**
```json
{
  "success": true,
  "data": {
    "predictions": [
      {
        "id": "pred_789",
        "date": "2024-01-21T14:00:00Z",
        "probability": 75,
        "risk": "high",
        "contributingFactors": [
          "Historical pattern on Sundays",
          "Weather pressure change predicted",
          "Sleep deficit detected"
        ],
        "confidence": 0.82
      },
      {
        "id": "pred_790",
        "date": "2024-01-22T10:00:00Z",
        "probability": 45,
        "risk": "medium",
        "contributingFactors": [
          "Recent stress levels",
          "Moderate risk based on weekly pattern"
        ],
        "confidence": 0.71
      }
    ],
    "modelVersion": "v2.1.0",
    "generatedAt": "2024-01-20T20:00:00Z"
  }
}
```

#### Get Prediction Accuracy

```http
GET /predictions/accuracy
Authorization: Bearer <token>
```

**Response:**
```json
{
  "success": true,
  "data": {
    "overallAccuracy": 0.78,
    "precision": 0.82,
    "recall": 0.75,
    "f1Score": 0.78,
    "totalPredictions": 120,
    "correctPredictions": 94,
    "lastUpdated": "2024-01-20T20:00:00Z"
  }
}
```

### Statistics

#### Get User Statistics

```http
GET /statistics
Authorization: Bearer <token>

Query Parameters:
- period: 'week' | 'month' | 'year' | 'all' (default: 'month')
- startDate: ISO 8601 date
- endDate: ISO 8601 date
```

**Response:**
```json
{
  "success": true,
  "data": {
    "period": "month",
    "startDate": "2024-01-01T00:00:00Z",
    "endDate": "2024-01-31T23:59:59Z",
    "totalEpisodes": 12,
    "averageIntensity": 6.5,
    "averageDuration": 480,
    "currentStreak": 3,
    "longestStreak": 7,
    "weeklyAverage": 2.5,
    "mostCommonTriggers": [
      { "name": "Stress", "count": 8 },
      { "name": "Sleep", "count": 6 },
      { "name": "Weather", "count": 4 }
    ],
    "mostCommonSymptoms": [
      { "name": "Nausea", "count": 9 },
      { "name": "Sensitivity to Light", "count": 7 },
      { "name": "Sensitivity to Sound", "count": 5 }
    ],
    "episodesByDay": {
      "Monday": 2,
      "Tuesday": 1,
      "Wednesday": 3,
      "Thursday": 1,
      "Friday": 2,
      "Saturday": 2,
      "Sunday": 1
    },
    "episodesByHour": {
      "0-6": 1,
      "6-12": 4,
      "12-18": 5,
      "18-24": 2
    }
  }
}
```

#### Get Trends

```http
GET /statistics/trends
Authorization: Bearer <token>

Query Parameters:
- metric: 'frequency' | 'intensity' | 'duration'
- period: 'week' | 'month' | 'year'
```

**Response:**
```json
{
  "success": true,
  "data": {
    "metric": "intensity",
    "period": "month",
    "dataPoints": [
      { "date": "2024-01-01", "value": 7 },
      { "date": "2024-01-05", "value": 6 },
      { "date": "2024-01-12", "value": 8 },
      { "date": "2024-01-20", "value": 7 }
    ],
    "trend": "stable",
    "trendPercentage": 2.5,
    "average": 7.0
  }
}
```

### Settings

#### Get User Settings

```http
GET /settings
Authorization: Bearer <token>
```

**Response:**
```json
{
  "success": true,
  "data": {
    "notifications": {
      "enabled": true,
      "pushNotifications": true,
      "emailNotifications": false,
      "reminderAlerts": false,
      "predictionAlerts": true
    },
    "privacy": {
      "analytics": true,
      "dataSharing": false
    },
    "preferences": {
      "theme": "auto",
      "language": "en",
      "timeZone": "America/New_York",
      "units": "imperial"
    }
  }
}
```

#### Update Settings

```http
PATCH /settings
Authorization: Bearer <token>
```

**Request Body:**
```json
{
  "notifications": {
    "pushNotifications": false,
    "reminderAlerts": true
  }
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "notifications": {
      "enabled": true,
      "pushNotifications": false,
      "emailNotifications": false,
      "reminderAlerts": true,
      "predictionAlerts": true
    },
    "updatedAt": "2024-01-20T15:00:00Z"
  }
}
```

## Data Models

### Episode Model

```typescript
interface Episode {
  id: string;
  userId: string;
  date: string; // ISO 8601
  intensity: number; // 1-10
  duration: number; // minutes
  triggers: string[];
  symptoms: string[];
  notes?: string;
  createdAt: string; // ISO 8601
  updatedAt: string; // ISO 8601
}
```

### Prediction Model

```typescript
interface Prediction {
  id: string;
  date: string; // ISO 8601
  probability: number; // 0-100
  risk: 'low' | 'medium' | 'high';
  contributingFactors?: string[];
  confidence: number; // 0-1
}
```

### Statistics Model

```typescript
interface Statistics {
  period: 'week' | 'month' | 'year' | 'all';
  startDate: string;
  endDate: string;
  totalEpisodes: number;
  averageIntensity: number;
  averageDuration: number;
  currentStreak: number;
  longestStreak: number;
  weeklyAverage: number;
  mostCommonTriggers: { name: string; count: number }[];
  mostCommonSymptoms: { name: string; count: number }[];
  episodesByDay: Record<string, number>;
  episodesByHour: Record<string, number>;
}
```

## Error Handling

### Error Response Format

```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {
      "field": "specific field error"
    }
  }
}
```

### Common Error Codes

| Code | Status | Description |
|------|--------|-------------|
| `UNAUTHORIZED` | 401 | Invalid or missing authentication token |
| `FORBIDDEN` | 403 | User doesn't have permission |
| `NOT_FOUND` | 404 | Resource not found |
| `VALIDATION_ERROR` | 400 | Invalid request data |
| `RATE_LIMIT_EXCEEDED` | 429 | Too many requests |
| `INTERNAL_ERROR` | 500 | Server error |
| `SERVICE_UNAVAILABLE` | 503 | Service temporarily unavailable |

### Example Error Response

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid episode data",
    "details": {
      "intensity": "Must be between 1 and 10",
      "date": "Must be a valid ISO 8601 date"
    }
  }
}
```

## Rate Limiting

### Rate Limits

- **Authenticated requests**: 100 requests per minute
- **Unauthenticated requests**: 10 requests per minute
- **Prediction endpoint**: 20 requests per hour

### Rate Limit Headers

```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1642697400
```

### Rate Limit Exceeded Response

```json
{
  "success": false,
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "Too many requests. Please try again later.",
    "retryAfter": 60
  }
}
```

## Versioning

The API uses URL versioning:

```
/v1/episodes
/v2/episodes
```

### Version Support

- **v1**: Current version (stable)
- Backward compatibility maintained for at least 6 months after new version release
- Deprecated endpoints will include `Deprecated` header

### Deprecation Header

```
Deprecated: true
Sunset: Sat, 01 Jul 2024 00:00:00 GMT
Link: </v2/episodes>; rel="successor-version"
```

## Best Practices

### Request Best Practices

1. **Always include authentication token** for protected endpoints
2. **Use HTTPS** in production
3. **Handle pagination** for list endpoints
4. **Implement retry logic** with exponential backoff
5. **Cache responses** when appropriate
6. **Validate data** before sending requests

### Error Handling Best Practices

```typescript
// Example error handling in React Native
async function createEpisode(episodeData) {
  try {
    const response = await fetch(`${API_BASE_URL}/episodes`, {
      method: 'POST',
      headers: {
        'Authorization': `Bearer ${token}`,
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(episodeData),
    });
    
    const data = await response.json();
    
    if (!response.ok) {
      throw new Error(data.error.message);
    }
    
    return data.data;
  } catch (error) {
    // Handle network errors, validation errors, etc.
    console.error('Failed to create episode:', error);
    throw error;
  }
}
```

## Future Enhancements

- **GraphQL API**: Alternative to REST
- **WebSocket support**: Real-time updates
- **Batch operations**: Bulk create/update/delete
- **Export data**: CSV/JSON export
- **Data import**: Import from other platforms
- **Webhooks**: Event notifications

## Support

For API-related questions or issues:
- Open an issue on GitHub
- Contact: api-support@migrainetracker.app
- Documentation: https://docs.migrainetracker.app

---

**API Version**: v1.0.0  
**Last Updated**: November 2024
