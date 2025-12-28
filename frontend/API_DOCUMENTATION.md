# StreamVibe - API Documentation

## API Overview

This document describes the API endpoints used by the StreamVibe frontend application. All API calls are made to the backend API base URL configured in `NEXT_PUBLIC_API_URL`.

## Base URL

All endpoints are relative to: `${NEXT_PUBLIC_API_URL}`

Example: `http://localhost:3001/api` or `https://api.streamvibe.com/api`

## Authentication

Most endpoints require authentication using cookie-based sessions. Include credentials in requests:

```javascript
fetch(`${API_URL}/endpoint`, {
  credentials: 'include'
});
```

## API Endpoints

### Movies

#### Get Movie Categories
```
GET /movie/categories
```

**Description**: Fetch all available movie categories

**Response**:
```json
[
  {
    "id": 1,
    "name": "Action",
    "slug": "action"
  },
  ...
]
```

**Service Function**: `MovieService.fetchMovieCategories()`

---

#### Get Top Rated Movies
```
GET /movie/top-rated?limit=4
```

**Description**: Fetch top-rated movies

**Query Parameters**:
- `limit` (optional): Number of movies to return (default: 4)

**Response**:
```json
{
  "movies": [
    {
      "id": 1,
      "title": "Movie Title",
      "slug": "movie-slug",
      "rating": 8.5,
      "thumbnail": "url",
      ...
    }
  ]
}
```

**Service Function**: `MovieService.fetchTopRatedCategories()`

---

#### Get Trending Movies
```
GET /movie/trending-movies?page=1
```

**Description**: Fetch trending movies with pagination

**Query Parameters**:
- `page` (optional): Page number (default: 1)

**Response**:
```json
{
  "movies": [...],
  "currentPage": 1,
  "totalPages": 10,
  "totalMovies": 100
}
```

**Service Function**: `MovieService.getTrendingMovies(page)`

---

#### Get New Released Movies
```
GET /movie/new-released?page=1
```

**Description**: Fetch newly released movies

**Query Parameters**:
- `page` (optional): Page number (default: 1)

**Response**: Same format as trending movies

**Service Function**: `MovieService.getNewReleasedMovies(page)`

---

#### Get Popular Movies
```
GET /movie/popular-movies?page=1
```

**Description**: Fetch popular movies

**Query Parameters**:
- `page` (optional): Page number (default: 1)

**Response**: Same format as trending movies

**Service Function**: `MovieService.getPopularMovies(page)`

---

#### Get Single Movie
```
GET /movie/{slug}
```

**Description**: Fetch detailed information for a single movie

**Path Parameters**:
- `slug`: Movie slug/identifier

**Response**:
```json
{
  "id": 1,
  "title": "Movie Title",
  "slug": "movie-slug",
  "description": "Movie description",
  "rating": 8.5,
  "releaseDate": "2024-01-01",
  "duration": 120,
  "genres": [...],
  "languages": [...],
  "director": {...},
  "cast": [...],
  "downloadLinks": [...],
  ...
}
```

**Service Function**: `MovieService.fetchSingleMovies(slug)`

---

#### Get Movies by Genre
```
GET /movie/moviesByGenre/{genre}?page=1&topRated=false
```

**Description**: Fetch movies filtered by genre

**Path Parameters**:
- `genre`: Genre name or slug

**Query Parameters**:
- `page` (optional): Page number (default: 1)
- `topRated` (optional): Filter by top rated (default: false)

**Response**: Same format as trending movies

**Service Function**: `MovieService.fetchGenreMovies(genre, page, topRated)`

---

#### Download Movie
```
POST /movie/download
```

**Description**: Download a movie file

**Request Body**:
```json
{
  "url": "https://example.com/movie.mp4"
}
```

**Response**: File download response

**Service Function**: `MovieService.downloadMovieApi(url)`

**Authentication**: Required

---

### TV Series

#### Get Series Categories
```
GET /series/categories
```

**Description**: Fetch all available series categories

**Response**: Same format as movie categories

---

#### Get Trending Series
```
GET /series/trending-series?page=1
```

**Description**: Fetch trending TV series

**Query Parameters**:
- `page` (optional): Page number

**Response**: Same format as trending movies

---

#### Get New Released Series
```
GET /series/new-released?page=1
```

**Description**: Fetch newly released series

**Query Parameters**:
- `page` (optional): Page number

**Response**: Same format as trending movies

---

#### Get Popular Series
```
GET /series/popular-series?page=1
```

**Description**: Fetch popular TV series

**Query Parameters**:
- `page` (optional): Page number

**Response**: Same format as trending movies

---

#### Get Single Series
```
GET /series/{slug}
```

**Description**: Fetch detailed information for a single series

**Path Parameters**:
- `slug`: Series slug/identifier

**Response**:
```json
{
  "id": 1,
  "title": "Series Title",
  "slug": "series-slug",
  "description": "Series description",
  "rating": 8.5,
  "releaseDate": "2024-01-01",
  "seasons": [
    {
      "id": 1,
      "seasonNumber": 1,
      "episodes": [...]
    }
  ],
  ...
}
```

---

#### Get Series Seasons
```
GET /series/{seriesId}/seasons
```

**Description**: Fetch all seasons for a series

**Path Parameters**:
- `seriesId`: Series ID

**Response**:
```json
{
  "seasons": [
    {
      "id": 1,
      "seasonNumber": 1,
      "episodeCount": 10,
      ...
    }
  ]
}
```

---

#### Get Series Episodes
```
GET /series/seasons/{seasonId}/episodes
```

**Description**: Fetch episodes for a season

**Path Parameters**:
- `seasonId`: Season ID

**Response**:
```json
{
  "episodes": [
    {
      "id": 1,
      "episodeNumber": 1,
      "title": "Episode Title",
      "description": "...",
      "duration": 45,
      ...
    }
  ]
}
```

---

#### Get Series by Genre
```
GET /series/seriesByGenre/{genre}?page=1&topRated=false
```

**Description**: Fetch series filtered by genre

**Path Parameters**:
- `genre`: Genre name or slug

**Query Parameters**:
- `page` (optional): Page number
- `topRated` (optional): Filter by top rated

**Response**: Same format as trending movies

---

### Actors

#### Get Actors
```
GET /actors?page=1
```

**Description**: Fetch list of actors

**Query Parameters**:
- `page` (optional): Page number

**Response**:
```json
{
  "actors": [
    {
      "id": 1,
      "name": "Actor Name",
      "slug": "actor-slug",
      "profileImage": "url",
      ...
    }
  ],
  "currentPage": 1,
  "totalPages": 10
}
```

---

#### Get Single Actor
```
GET /actors/{slug}
```

**Description**: Fetch detailed actor information

**Path Parameters**:
- `slug`: Actor slug/identifier

**Response**:
```json
{
  "id": 1,
  "name": "Actor Name",
  "slug": "actor-slug",
  "bio": "Actor biography",
  "profileImage": "url",
  "movies": [...],
  ...
}
```

---

#### Get Actor Movies
```
GET /actors/{actorId}/movies?page=1
```

**Description**: Fetch movies featuring the actor

**Path Parameters**:
- `actorId`: Actor ID

**Query Parameters**:
- `page` (optional): Page number

**Response**: Same format as trending movies

---

#### Search Actors
```
GET /actors/search?q={query}
```

**Description**: Search actors by name

**Query Parameters**:
- `q`: Search query

**Response**:
```json
{
  "actors": [...]
}
```

---

### Directors

#### Get Directors
```
GET /directors?page=1
```

**Description**: Fetch list of directors

**Query Parameters**:
- `page` (optional): Page number

**Response**: Same format as actors

---

#### Get Single Director
```
GET /directors/{slug}
```

**Description**: Fetch detailed director information

**Path Parameters**:
- `slug`: Director slug/identifier

**Response**: Same format as single actor

---

#### Get Director Movies
```
GET /directors/{directorId}/movies?page=1
```

**Description**: Fetch movies directed by the director

**Path Parameters**:
- `directorId`: Director ID

**Query Parameters**:
- `page` (optional): Page number

**Response**: Same format as trending movies

---

#### Search Directors
```
GET /directors/search?q={query}
```

**Description**: Search directors by name

**Query Parameters**:
- `q`: Search query

**Response**: Same format as actor search

---

### Reviews

#### Get Reviews
```
GET /reviews?contentId={id}&contentType={type}
```

**Description**: Fetch reviews for content

**Query Parameters**:
- `contentId`: Content ID (movie or series)
- `contentType`: Content type ("movie" or "series")

**Response**:
```json
{
  "reviews": [
    {
      "id": 1,
      "userId": 1,
      "userName": "User Name",
      "rating": 5,
      "comment": "Review text",
      "createdAt": "2024-01-01T00:00:00Z",
      ...
    }
  ]
}
```

---

#### Add Review
```
POST /reviews
```

**Description**: Add a new review

**Request Body**:
```json
{
  "contentId": 1,
  "contentType": "movie",
  "rating": 5,
  "comment": "Great movie!"
}
```

**Response**: Created review object

**Authentication**: Required

---

#### Update Review
```
PUT /reviews/{reviewId}
```

**Description**: Update existing review

**Path Parameters**:
- `reviewId`: Review ID

**Request Body**:
```json
{
  "rating": 4,
  "comment": "Updated review"
}
```

**Response**: Updated review object

**Authentication**: Required (own reviews only)

---

#### Delete Review
```
DELETE /reviews/{reviewId}
```

**Description**: Delete a review

**Path Parameters**:
- `reviewId`: Review ID

**Response**: Success message

**Authentication**: Required (own reviews only)

---

### Likes/Favorites

#### Like Content
```
POST /likes
```

**Description**: Like/favorite content

**Request Body**:
```json
{
  "contentId": 1,
  "contentType": "movie"
}
```

**Response**: Success message

**Authentication**: Required

---

#### Unlike Content
```
DELETE /likes?contentId={id}&contentType={type}
```

**Description**: Remove like/favorite

**Query Parameters**:
- `contentId`: Content ID
- `contentType`: Content type

**Response**: Success message

**Authentication**: Required

---

#### Check Like Status
```
GET /likes/status?contentId={id}&contentType={type}
```

**Description**: Check if content is liked

**Query Parameters**:
- `contentId`: Content ID
- `contentType`: Content type

**Response**:
```json
{
  "isLiked": true
}
```

**Authentication**: Required

---

#### Get Liked Content
```
GET /likes?userId={id}
```

**Description**: Fetch user's liked content

**Query Parameters**:
- `userId`: User ID

**Response**:
```json
{
  "movies": [...],
  "series": [...]
}
```

**Authentication**: Required

---

### Subscriptions

#### Get Subscription Plans
```
GET /subscriptions/plans
```

**Description**: Fetch available subscription plans

**Response**:
```json
{
  "plans": [
    {
      "id": 1,
      "name": "Basic",
      "price": 9.99,
      "duration": "monthly",
      "features": [...],
      ...
    }
  ]
}
```

---

#### Subscribe
```
POST /subscriptions
```

**Description**: Subscribe user to a plan

**Request Body**:
```json
{
  "planId": 1
}
```

**Response**: Subscription object

**Authentication**: Required

---

#### Get User Subscription
```
GET /subscriptions/current
```

**Description**: Fetch user's current subscription

**Response**:
```json
{
  "id": 1,
  "planId": 1,
  "planName": "Basic",
  "status": "active",
  "startDate": "2024-01-01",
  "endDate": "2024-02-01",
  ...
}
```

**Authentication**: Required

---

#### Update Subscription
```
PUT /subscriptions
```

**Description**: Update subscription plan

**Request Body**:
```json
{
  "planId": 2
}
```

**Response**: Updated subscription object

**Authentication**: Required

---

#### Cancel Subscription
```
DELETE /subscriptions
```

**Description**: Cancel user subscription

**Response**: Success message

**Authentication**: Required

---

### User

#### Get User Data
```
GET /user/userData
```

**Description**: Fetch current user data

**Response**:
```json
{
  "user": {
    "id": 1,
    "name": "User Name",
    "email": "user@example.com",
    "avatar": "url",
    ...
  }
}
```

**Authentication**: Required

---

#### Register
```
POST /user/register
```

**Description**: Register a new user

**Request Body**:
```json
{
  "name": "User Name",
  "email": "user@example.com",
  "password": "password123"
}
```

**Response**: User object and authentication cookie

---

#### Login
```
POST /user/login
```

**Description**: Login user

**Request Body**:
```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

**Response**: User object and authentication cookie

---

#### Logout
```
POST /user/logout
```

**Description**: Logout user

**Response**: Success message

**Authentication**: Required

---

### Support

#### Submit Support Form
```
POST /support
```

**Description**: Submit support/contact form

**Request Body**:
```json
{
  "name": "User Name",
  "email": "user@example.com",
  "subject": "Support Request",
  "message": "Support message"
}
```

**Response**: Success message

---

#### Get Support Tickets
```
GET /support/tickets?userId={id}
```

**Description**: Fetch user's support tickets

**Query Parameters**:
- `userId`: User ID

**Response**:
```json
{
  "tickets": [
    {
      "id": 1,
      "subject": "Support Request",
      "status": "open",
      "createdAt": "2024-01-01T00:00:00Z",
      ...
    }
  ]
}
```

**Authentication**: Required

---

## Error Responses

All endpoints may return error responses in the following format:

```json
{
  "error": "Error message",
  "statusCode": 400
}
```

### Common Status Codes

- `200` - Success
- `201` - Created
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not Found
- `500` - Internal Server Error

## Rate Limiting

API endpoints may have rate limiting. Check response headers for rate limit information:
- `X-RateLimit-Limit`: Request limit
- `X-RateLimit-Remaining`: Remaining requests
- `X-RateLimit-Reset`: Reset time

## Pagination

Endpoints that support pagination return data in this format:

```json
{
  "data": [...],
  "currentPage": 1,
  "totalPages": 10,
  "totalItems": 100,
  "itemsPerPage": 10
}
```

## CORS

The API should be configured to allow requests from the frontend domain. CORS headers should include:
- `Access-Control-Allow-Origin`: Frontend domain
- `Access-Control-Allow-Credentials`: true (for cookie-based auth)

## Notes

- All dates are in ISO 8601 format
- All image URLs should be absolute URLs
- Pagination starts at page 1
- Default page size is typically 10-20 items

