# Hopper

Hopper is a lightweight URL shortener service built using Go and the Fiber web framework. It provides a simple REST API to create shortened URLs and resolve them back to their original destinations.

The project is structured for containerized deployment using Docker Compose and is designed as a clean, minimal backend service.

---

## Features

- Create short URLs from long URLs
- Resolve short URLs via HTTP redirect
- Environment-based configuration
- Structured routing using Fiber
- Request logging middleware
- Docker Compose support for local development

---

## Tech Stack

- **Go**
- **Fiber** (v2)
- **Docker**
- **Docker Compose**
- **godotenv** (environment configuration)

---

## Project Structure

```
.
├── api/
│   ├── main.go
│   └── routes/
├── db/
├── docker-compose.yml
├── go.mod
├── go.sum
└── .gitignore
```

| Path | Description |
|---|---|
| `api/` | Application source code |
| `api/routes/` | Route handlers (URL shortening and resolution) |
| `db/` | Database configuration or initialization scripts |
| `docker-compose.yml` | Container orchestration setup |
| `go.mod` / `go.sum` | Go dependency management |

---

## API Endpoints

### 1. Create Short URL

```
POST /api/v1
```

**Request Body**

```json
{
  "url": "https://example.com/some/long/path"
}
```

**Response**

```json
{
  "shortUrl": "http://localhost:3000/abc123"
}
```

---

### 2. Resolve Short URL

```
GET /:url
```

**Example**

```
GET /abc123
```

Redirects (typically `301` or `302`) to the original URL associated with the short code.

---

## Environment Variables

Create a `.env` file in the project root:

```env
APP_PORT=:3000
```

> Additional environment variables may be required depending on your database implementation.

---

## Running Locally

### Option 1: Using Go

1. Install [Go](https://golang.org/dl/) (1.18+ recommended)
2. Clone the repository:

```bash
git clone https://github.com/Kshitij-Jain99/hopper.git
cd hopper
```

3. Install dependencies:

```bash
go mod download
```

4. Run the application:

```bash
go run api/main.go
```

The server will start on the port defined in `.env`.

---

### Option 2: Using Docker Compose

Make sure [Docker](https://www.docker.com/) and Docker Compose are installed, then run:

```bash
docker-compose up --build
```

This will start the application (and database if configured).

---

## Example cURL Requests

**Create a short URL**

```bash
curl -X POST http://localhost:3000/api/v1 \
  -H "Content-Type: application/json" \
  -d '{"url":"https://example.com"}'
```

**Resolve a short URL**

```bash
curl -L http://localhost:3000/abc123
```

---

## Future Improvements

- Input validation and URL sanitization
- Rate limiting
- Database migrations
- Unit and integration tests
- Analytics (click tracking)
- Custom aliases
- Expiration support
- API documentation (OpenAPI/Swagger)

---
