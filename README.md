# Weather API

Node.js + Express backend that returns the current weather for a city, using the OpenWeatherMap API.

## Features

- Layered structure: routes → controller → service → API client
- Request validation with express-validator
- Centralized error handling with a consistent JSON error format
- Configuration check on startup: the server exits with a clear message if the API key is missing

## Tech stack

Node.js · Express 5 · axios · express-validator · dotenv · Docker

## Getting started

```bash
git clone https://github.com/AmanImanzhan/WeatherApiFirst.git
cd WeatherApiFirst
npm install
cp .env.example .env     # then add your OpenWeatherMap API key
npm run dev
```

A free API key can be created at https://openweathermap.org/api. The server starts on `http://localhost:3000` by default.

### Run with Docker

```bash
cp .env.example .env     # set OPENWEATHER_API_KEY and PORT=3000
docker compose up --build
```

## Environment variables

| Variable | Required | Description |
|---|---|---|
| `OPENWEATHER_API_KEY` | yes | OpenWeatherMap API key |
| `PORT` | no | Server port (default `3000`) |
| `WEATHER_API_URL` | no | Override the OpenWeatherMap endpoint |

## API

### `GET /api/weather?city=London`

Success response:

```json
{
  "success": true,
  "data": {
    "city": "London",
    "temperature": 14,
    "description": "light rain"
  }
}
```

Errors use the format `{ "error": { "message": "..." } }`. Invalid input returns `400`, unknown routes return `404`.

## Project structure

```
src/
├── api/weatherApiClient.js        # OpenWeatherMap client
├── config/config.js               # env loading and validation
├── domain/entities/weather.js     # Weather entity
├── modules/weather/               # routes, controller, service, validation
└── utils/errorHandler.js          # centralized error handling
```
