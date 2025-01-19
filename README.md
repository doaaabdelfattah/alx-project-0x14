# MoviesDatabase API Documentation

## API Overview

The MoviesDatabase API provides developers with an extensive set of features to interact with movie data. The API supports fetching movie details, searching for movies, retrieving genres, and accessing trending or popular movies.

### Key Features:

- **Movie Details**: Retrieve detailed information such as title, release date, genres, and ratings.
- **Search Functionality**: Search for movies by title, genre, or release year.
- **Genres**: Access a list of available movie genres.
- **Popular Movies**: Fetch trending and popular movie lists.
- **Response Format**: All responses are in JSON format for easy integration.

---

## API Version

## The current API version is **v3.0**.

## Available Endpoints

Below is a list of the main endpoints offered by the API:

1. **`GET /movies/{id}`**

   - **Description**: Fetch detailed information about a movie by its ID.
   - **Example**: `/movies/12345`

2. **`GET /search`**

   - **Description**: Search for movies by title, genre, or release year.
   - **Parameters**:
     - `title` (optional): Search by movie title.
     - `genre` (optional): Filter by genre.
     - `year` (optional): Filter by release year.

3. **`GET /genres`**

   - **Description**: Retrieve a list of all available movie genres.
   - **Example**: `/genres`

4. **`GET /popular`**
   - **Description**: Get a list of trending or popular movies.
   - **Example**: `/popular`

---

## Request and Response Format

### Request Format

Requests are made to the API using standard HTTP methods (`GET`, `POST`, etc.). Include your API key in the headers or as a query parameter.

#### Example Request

```http
GET /movies/12345 HTTP/1.1
Host: api.moviesdatabase.com
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

## Authentication

````
curl --request GET \
     --url 'https://api.themoviedb.org/3/movie/11' \
     --header 'Authorization: Bearer "YOUR API KEY"'
     ```
````

## Error Handling

- 401 Unauthorized
  The request lacks valid authentication credentials (e.g., missing or invalid API key).
  Example Response:

```
{
  "error": "Unauthorized",
  "message": "Invalid API key."
}
```

**How to Handle:**

1. Verify that the API key is included in the request.
2. Check if the API key has expired or been revoked.
3. Provide clear feedback to the user, such as prompting them to log in again.

- 404 Not Found
  The requested resource (e.g., movie ID) does not exist.
  Example Response:

```
{
  "error": "Not Found",
  "message": "The movie ID does not exist."
}
```

**How to Handle:**

1. Check the request URL and parameters for typos or incorrect values.
2. Notify the user that the requested resource is unavailable.

- 429 Too Many Requests
  The API rate limit has been exceeded.

```
{
  "error": "Rate Limit Exceeded",
  "message": "You have exceeded the allowed number of requests."
}
```

**How to Handle:**

1. Implement request throttling or backoff strategies (e.g., retry after a delay).
2. Log excessive usage to optimize future requests.
3. Inform the user to try again later.

## Usage Limits and Best Practices

APIs often impose usage restrictions to ensure fair usage and server stability. Understanding these limits helps you design efficient and compliant applications.

### Usage Limits

- Rate Limits:
  Most APIs limit the number of requests per second, minute, or day.
  Example: "You can make up to 1,000 requests per day with a single API key."
  If you exceed this limit, you’ll typically receive a 429 Too Many Requests response.

- Data Limits:
  Some APIs restrict the amount of data that can be returned in a single response.
  Pagination is often required for large datasets.

- Request Size:
  APIs may limit the size of payloads (e.g., maximum request body size for POST requests).

### Best Practices

- Optimize API Calls:
  Fetch only the data you need by using filters, query parameters, or specific fields.
  Example: Use /movies?fields=title,release_date instead of fetching all movie details.

- Implement Caching:
  Cache responses from endpoints that return static or infrequently updated data (e.g., genres list).
  This reduces unnecessary API calls and improves performance.

- Handle Rate Limits Gracefully:
  When approaching the rate limit, reduce the frequency of requests or pause operations until the limit resets.
  Use the Retry-After header (if provided by the API) to determine when to retry.

- Use Pagination:
  When fetching large datasets, utilize pagination to process data in manageable chunks.
  Example: /movies?page=1&limit=10

- Secure Your API Key:
  Store API keys securely (e.g., in environment variables).
  Do not expose API keys in client-side code.
