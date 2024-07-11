# URL Shortener API in Go

This is a URL Shortener API built with Go, Fiber, Redis, and Docker. It allows you to shorten URLs and handle custom short URLs with an expiry time. The project also includes rate limiting to control the number of requests from a single IP address.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Environment Variables](#environment-variables)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
  - [Shorten URL](#shorten-url)
  - [Resolve URL](#resolve-url)

## Prerequisites

- [Go](https://golang.org/doc/install)
- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [Redis](https://redis.io/download) (if running locally without Docker)

## Installation

1. Clone the repository:

```bash
git clone https://github.com/itisohm/url-shortener-go.git
cd url-shortener-go
```
2. Set up environment variables:
Create a .env file in the root directory of the project and add the necessary environment variables (see [Environment Variables](#environment-variables)).

3. Build and run the application using Docker Compose:
   
```bash
docker-compose up --build
```
This will start the application and Redis in separate Docker containers.

## Environment Variables
Create a .env file in the root directory with the following content:
```bash
DB_ADDR = "db:6379"
DB_PASS = ""
APP_PORT = ":3000"
DOMAIN = "http://localhost:8080"
API_QUOTA = 10
```

## Usage
Once the application is up and running, you can access the API at `http://localhost:8080`

## API Endpoints
1. Shorten URL:
- URL: `/api/v1`
- Method: `POST`
- Request Body:

```bash
{
  "url" : "https://www.youtube.com/watch?v=dQw4w9WgXcQ"
}
```
- Response:

```bash
{
  "url": "https://example.com", // Original URL.
  "customShort": "http://localhost:8080/custom", // Custom shortened URL.
  "expiry": 24, // Expiry time in hours.
  "rateRem": 9, // Number of queries remaining.
  "rateLmtRst": 30 // Rate limit reset time in minutes.
}
```

2. Resolve URL:
- URL: `/:url`
- Method: `GET`
- Response: Redirects to the original URL.
