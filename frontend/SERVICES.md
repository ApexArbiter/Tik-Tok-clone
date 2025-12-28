# StreamVibe - Services Documentation

## Services Overview

The services layer in StreamVibe handles all API communication with the backend. Each service is organized by domain and contains functions for making HTTP requests to the API endpoints.

## Service Architecture

All services follow a consistent pattern:
- Use `fetch` API for HTTP requests
- Base URL from `process.env.NEXT_PUBLIC_API_URL`
- Error handling with try-catch blocks
- Return data in a consistent format

## Service Files

### MovieService.js

Handles all movie-related API operations.

#### Functions

**fetchMovieCategories()**
- **Purpose**: Fetch all movie categories
- **Endpoint**: `GET /movie/categories`
- **Returns**: Array of movie categories
- **Error Handling**: Returns empty array on error

```javascript
const categories = await fetchMovieCategories();
```

**fetchTopRatedCategories()**
- **Purpose**: Fetch top-rated movies
- **Endpoint**: `GET /movie/top-rated?limit=4`
- **Returns**: Array of top-rated movies
- **Error Handling**: Throws error if request fails

```javascript
const topRated = await fetchTopRatedCategories();
```

**getTrendingMovies(currentPage, page)**
- **Purpose**: Fetch trending movies with pagination
- **Endpoint**: `GET /movie/trending-movies?page={page}`
- **Parameters**: 
  - `currentPage` (optional) - Current page number
  - `page` (optional) - Page number (fallback)
- **Returns**: Paginated movie data
- **Error Handling**: Returns empty array on error

```javascript
const trending = await getTrendingMovies(1);
```

**getNewReleasedMovies(currentPage, page)**
- **Purpose**: Fetch newly released movies
- **Endpoint**: `GET /movie/new-released?page={page}`
- **Parameters**: Same as getTrendingMovies
- **Returns**: Paginated movie data
- **Error Handling**: Logs error, returns undefined

```javascript
const newReleases = await getNewReleasedMovies(1);
```

**getPopularMovies(currentPage, page)**
- **Purpose**: Fetch popular movies
- **Endpoint**: `GET /movie/popular-movies?page={page}`
- **Parameters**: Same as getTrendingMovies
- **Returns**: Paginated movie data
- **Error Handling**: Logs error, returns undefined

```javascript
const popular = await getPopularMovies(1);
```

**fetchSingleMovies(slug)**
- **Purpose**: Fetch single movie details
- **Endpoint**: `GET /movie/{slug}`
- **Parameters**: 
  - `slug` - Movie slug/identifier
- **Returns**: Movie details object
- **Error Handling**: Returns error response

```javascript
const movie = await fetchSingleMovies('movie-slug');
```

**downloadMovieApi(url)**
- **Purpose**: Download a movie file
- **Endpoint**: `POST /movie/download`
- **Parameters**: 
  - `url` - Movie download URL
- **Request Body**: `{ url: string }`
- **Returns**: Response object
- **Error Handling**: Logs error, returns undefined

```javascript
const response = await downloadMovieApi('https://...');
```

**fetchGenreMovies(genre, currentPage, page, topRated)**
- **Purpose**: Fetch movies by genre
- **Endpoint**: `GET /movie/moviesByGenre/{genre}?page={page}&topRated={topRated}`
- **Parameters**: 
  - `genre` - Genre name/slug
  - `currentPage` (optional) - Current page number
  - `page` (optional) - Page number (fallback)
  - `topRated` (optional) - Filter by top rated
- **Returns**: Paginated movie data
- **Error Handling**: Returns empty array on error

```javascript
const genreMovies = await fetchGenreMovies('action', 1, 1, false);
```

### SeriesService.js

Handles all TV series-related API operations.

#### Functions (Expected)

- `fetchSeriesCategories()` - Fetch series categories
- `getTrendingSeries(page)` - Fetch trending series
- `getNewReleasedSeries(page)` - Fetch new series
- `getPopularSeries(page)` - Fetch popular series
- `fetchSingleSeries(slug)` - Fetch series details
- `fetchSeriesSeasons(seriesId)` - Fetch seasons for a series
- `fetchSeriesEpisodes(seasonId)` - Fetch episodes for a season
- `fetchGenreSeries(genre, page)` - Fetch series by genre

### ActorService.js

Handles actor-related API operations.

#### Functions (Expected)

- `fetchActors(page)` - Fetch list of actors
- `fetchSingleActor(slug)` - Fetch actor details
- `fetchActorMovies(actorId, page)` - Fetch movies by actor
- `searchActors(query)` - Search actors by name

### DirectorService.js

Handles director-related API operations.

#### Functions (Expected)

- `fetchDirectors(page)` - Fetch list of directors
- `fetchSingleDirector(slug)` - Fetch director details
- `fetchDirectorMovies(directorId, page)` - Fetch movies by director
- `searchDirectors(query)` - Search directors by name

### ReviewService.js

Handles review and rating operations.

#### Functions (Expected)

- `fetchReviews(contentId, contentType)` - Fetch reviews for content
- `addReview(contentId, reviewData)` - Add a new review
- `updateReview(reviewId, reviewData)` - Update existing review
- `deleteReview(reviewId)` - Delete a review
- `fetchUserReviews(userId)` - Fetch reviews by a user

### LikeService.js

Handles like/favorite functionality.

#### Functions (Expected)

- `likeContent(contentId, contentType)` - Like content
- `unlikeContent(contentId, contentType)` - Unlike content
- `checkLikeStatus(contentId, contentType)` - Check if content is liked
- `fetchLikedContent(userId)` - Fetch user's liked content

### SubscriptionService.js

Handles subscription-related operations.

#### Functions (Expected)

- `fetchSubscriptionPlans()` - Fetch available subscription plans
- `subscribeUser(planId)` - Subscribe user to a plan
- `cancelSubscription()` - Cancel user subscription
- `fetchUserSubscription()` - Fetch user's current subscription
- `updateSubscription(planId)` - Update subscription plan

### SupportService.js

Handles support and contact form operations.

#### Functions (Expected)

- `submitSupportForm(formData)` - Submit support/contact form
- `fetchSupportTickets(userId)` - Fetch user's support tickets
- `fetchTicketDetails(ticketId)` - Fetch ticket details

## Service Usage Patterns

### Basic Usage

```javascript
import { fetchMovies } from '@/services/MovieService';

// In a component
const [movies, setMovies] = useState([]);

useEffect(() => {
  const loadMovies = async () => {
    const data = await fetchMovies();
    setMovies(data);
  };
  loadMovies();
}, []);
```

### With Error Handling

```javascript
import { fetchSingleMovies } from '@/services/MovieService';

const loadMovie = async (slug) => {
  try {
    const movie = await fetchSingleMovies(slug);
    if (movie) {
      setMovie(movie);
    } else {
      // Handle no data
      setError('Movie not found');
    }
  } catch (error) {
    setError('Failed to load movie');
    console.error(error);
  }
};
```

### With Loading States

```javascript
const [loading, setLoading] = useState(false);
const [data, setData] = useState(null);

const fetchData = async () => {
  setLoading(true);
  try {
    const result = await fetchMovies();
    setData(result);
  } catch (error) {
    // Handle error
  } finally {
    setLoading(false);
  }
};
```

### With Pagination

```javascript
const [page, setPage] = useState(1);
const [movies, setMovies] = useState([]);

const loadMovies = async (pageNum) => {
  const data = await getTrendingMovies(pageNum);
  setMovies(data.movies);
  setPage(data.currentPage);
};
```

## Authentication in Services

Services that require authentication should include credentials:

```javascript
const response = await fetch(`${API_URL}/protected-endpoint`, {
  method: 'GET',
  headers: {
    'Content-Type': 'application/json',
  },
  credentials: 'include' // Include cookies for auth
});
```

## Error Handling Best Practices

1. **Try-Catch Blocks**: Wrap all service calls in try-catch
2. **Error Logging**: Log errors for debugging
3. **User-Friendly Messages**: Return meaningful error messages
4. **Fallback Values**: Return empty arrays/objects on error
5. **Error States**: Set error state in components

## Service Testing

When testing services:
- Mock fetch API calls
- Test error scenarios
- Test success scenarios
- Test edge cases (empty responses, network errors)

## Environment Configuration

All services use `process.env.NEXT_PUBLIC_API_URL` for the base URL. Ensure this is set in:
- `.env.local` for local development
- `.env.production` for production
- Environment variables in deployment platform

## Future Enhancements

Consider adding:
1. **Request Interceptors**: For adding auth tokens
2. **Response Interceptors**: For handling common errors
3. **Retry Logic**: For failed requests
4. **Caching**: For frequently accessed data
5. **TypeScript**: For type safety
6. **Request Cancellation**: For aborting requests

