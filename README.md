# WeLoveMovies
### A comprehensive API for browsing movies, theaters and reviews. Follows RESTful API design principles.
> Live deployment is still being developed; will be updated soon.
<br />

## **Tech Stack:**
- Node.js: server environment for backend.
- Express: library for API development.
- Knex: manages API queries and connections.
- PostgreSQL: SQL database.
- ElephantSQL: host of PostgreSQL instance.

<br />

## **API Documentation**

<br />

### **GET /movies**

> This route returns all of the movies that exist in the database currently.

#### example:
```
{
  "data": [
    {
      "id": 1,
      "title": "Spirited Away",
      "runtime_in_minutes": 125,
      "rating": "PG",
      "description": "Chihiro ...",
      "image_url": "https://imdb-api.com/..."
    }
    ...
  ]
}
```

> In the event where "is_showing=true" is provided, the route will only return movies that are currently showing in theaters.

<br />

### **GET /movies/:movieId**

> This route will return a single movie by ID.

#### example:

```
{
  "data": {
    "id": 1,
    "title": "Spirited Away",
    "runtime_in_minutes": 125,
    "rating": "PG",
    "description": "Chihiro...",
    "image_url": "https://imdb-api.com/..."
  }
}
```

<br />

### **DELETE /reviews/:reviewId**

> This route will delete a review by ID. If the ID is incorrect, a 404 will be returned.

#### example (correct id):

> The server will respond with "204 No Content".

#### example (incorrect id):

```
{
  "error": "Review cannot be found."
}
```

<br />

### **PUT /reviews/:reviewId**

> This route will allow you to partially or fully update a review. If the ID is incorrect, a "404" will be returned.

#### A body like the following should be passed along with the request:

```
{
  "score": 3,
  "content": "New content..."
}
```

#### The response will include the entire review record with the newly patched content:

```
{
  "data": {
    "review_id": 1,
    "content": "New content...",
    "score": 3,
    "created_at": "2021-02-23T20:48:13.315Z",
    "updated_at": "2021-02-23T20:48:13.315Z",
    "critic_id": 1,
    "movie_id": 1,
    "critic": {
      "critic_id": 1,
      "preferred_name": "Chana",
      "surname": "Gibson",
      "organization_name": "Film Frenzy",
      "created_at": "2021-02-23T20:48:13.308Z",
      "updated_at": "2021-02-23T20:48:13.308Z"
    }
  }
}
```

<br />

### **GET /theaters**

> This route will return a list of all theaters.

### example:
```
{
  "data": [
    {
      "theater_id": 1,
      "name": "Regal City Center",
      "address_line_1": "801 C St.",
      "address_line_2": "",
      "city": "Vancouver",
      "state": "WA",
      "zip": "98660",
      "created_at": "2021-02-23T20:48:13.335Z",
      "updated_at": "2021-02-23T20:48:13.335Z",
      "movies": [
        {
          "movie_id": 1,
          "title": "Spirited Away",
          "runtime_in_minutes": 125,
          "rating": "PG",
          "description": "Chihiro...",
          "image_url": "https://imdb-api.com...",
          "created_at": "2021-02-23T20:48:13.342Z",
          "updated_at": "2021-02-23T20:48:13.342Z",
          "is_showing": false,
          "theater_id": 1
        }
        ...
      ]
    }
    ...
  ]
}
```

