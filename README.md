# GoIMDB API

GoIMDb API is a simple API for storing and retrieving movie data. The API is built using Go and Echo.

## Requirements

- Go 1.16 or later
- Echo v4
- RamSQL

## Installation

Clone the repository:

```bash
git clone https://github.com/nattrio/GoIMDb.git
```

Install dependencies:

```bash
go get github.com/labstack/echo/v4
go get github.com/labstack/echo/v4/middleware
go get github.com/erikstmartin/go-testdb
```

## Usage

Start the server:

```bash
go run main.go
```

or using Docker

```bash
docker build -t go-multi -f Dockerfile.multi .
docker run -d -p 2565:2565 --name go-multi go-multi
```

Use the following endpoints:

### `GET /movies`

Returns a list of all movies or all movies from a specific year if the `year` query parameter is provided.

#### Query Parameters

| Parameter | Description                         | Required |
| --------- | ----------------------------------- | -------- |
| `year`    | The year for which to return movies | No       |

#### Example Request

```http
GET /movies?year=2020
```

#### Example Response

```json
[
  {
    "id": 1,
    "imdbID": "tt0816692",
    "title": "Interstellar",
    "year": 2014,
    "rating": 8.6,
    "isSuperHero": false
  },
  {
    "id": 2,
    "imdbID": "tt1375666",
    "title": "Inception",
    "year": 2010,
    "rating": 8.8,
    "isSuperHero": false
  }
]
```

### `GET /movies/:imdbID`

Returns a specific movie.

#### URL Parameters

| Parameter | Description              | Required |
| --------- | ------------------------ | -------- |
| `imdbID`  | The IMDb ID of the movie | Yes      |

#### Example Request

```http
GET /movies/tt0816692
```

#### Example Response

```json
{
  "id": 1,
  "imdbID": "tt0816692",
  "title": "Interstellar",
  "year": 2014,
  "rating": 8.6,
  "isSuperHero": false
}
```

### `POST /movies`

Creates a new movie.

#### Request Body

| Field         | Type      | Description                                   |
| ------------- | --------- | --------------------------------------------- |
| `imdbID`      | `string`  | The IMDb ID of the movie                      |
| `title`       | `string`  | The title of the movie                        |
| `year`        | `int`     | The year the movie was released               |
| `rating`      | `float32` | The rating of the movie                       |
| `isSuperHero` | `bool`    | Whether or not the movie is a superhero movie |

#### Example Request

```http
POST /movies
Content-Type: application/json

{
    "imdbID": "tt0816692",
    "title": "Interstellar",
    "year": 2014,
    "rating": 8.6,
    "isSuperHero": false
}
```

#### Example Response

```json
{
  "id": 1,
  "imdbID": "tt0816692",
  "title": "Interstellar",
  "year": 2014,
  "rating": 8.6,
  "isSuperHero": false
}
```

### `PUT /movies/:imdbID`

Updates a specific movie's rating.
