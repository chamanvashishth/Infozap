# Infozap Backend Architecture Plan

## Ownership

- **Backend Developer:** [@chamanvashishth](https://github.com/chamanvashishth)
- **Primary stack:** Node.js, Express.js, MongoDB, and Mongoose
- **Goal:** Strengthen Infozap's server-side foundation so the platform can evolve from static current-affairs pages into a dynamic news ecosystem with scalable APIs, database-backed content, and future real-time integrations.

## Architecture Overview

Infozap uses a layered backend structure that separates HTTP concerns, request orchestration, persistence, and operational middleware:

```text
Client Pages / API Consumers
        |
        v
Express Application
        |
        +-- Middleware: CORS, JSON parsing, logging, error handling
        |
        +-- Routes: RESTful API resources under /api
        |
        +-- Controllers: Request validation and response formatting
        |
        +-- Models: Mongoose schemas for MongoDB collections
        |
        v
MongoDB Database
```

This structure keeps API endpoints predictable while making it easier to add moderation workflows, search, authentication, analytics, or external news-source integrations without tightly coupling those features to frontend pages.

## Current Backend Modules

| Layer | Location | Responsibility |
| --- | --- | --- |
| Application entry | `backend/server.js` | Configures Express, middleware, static files, API routes, health checks, and database connection handling. |
| Routes | `backend/routes/` | Defines RESTful endpoint groups, currently focused on posts and category lookups. |
| Controllers | `backend/controllers/` | Handles request processing, data normalization, MongoDB operations, and JSON responses. |
| Models | `backend/models/` | Stores MongoDB schema definitions for dynamic news data. |
| Middleware | `backend/middleware/` | Provides request logging, authentication hooks, and centralized error responses. |
| Deployment adapter | `api/[...all].js` | Exposes the Express app for serverless deployment environments such as Vercel. |

## RESTful API Plan

### Implemented Endpoints

| Method | Endpoint | Purpose |
| --- | --- | --- |
| `GET` | `/api` | Returns a lightweight API status message. |
| `GET` | `/api/health` | Returns operational health information for monitoring and deployment checks. |
| `GET` | `/api/posts` | Lists all posts sorted by latest publish date. |
| `POST` | `/api/posts` | Creates a dynamic news post in MongoDB. |
| `GET` | `/api/posts/:id` | Fetches a single post by MongoDB ObjectId. |
| `GET` | `/api/posts/category/:category` | Fetches posts by category with case-insensitive matching. |
| `PATCH` | `/api/posts/:id/like` | Increments a post's like count. |

### Planned Endpoint Expansion

| Resource | Candidate Endpoints | Notes |
| --- | --- | --- |
| Categories | `GET /api/categories`, `POST /api/categories` | Centralize category metadata, slugs, icons, and display ordering. |
| Search | `GET /api/search?q=&category=&limit=` | Support keyword, category, and date filters for faster discovery. |
| Authentication | `POST /api/auth/login`, `POST /api/auth/logout` | Protect compose and admin workflows. |
| Moderation | `PATCH /api/posts/:id/status` | Enable draft, review, published, archived, and rejected states. |
| Integrations | `POST /api/integrations/news/import` | Prepare ingestion from RSS feeds, public APIs, or editorial automation. |

## MongoDB Content Model

The post schema is designed for flexible news storage and supports:

- Required article metadata: `title`, `author`, and `newsContent`
- Discovery fields: `category`, `hashtags`, and `keywords`
- Presentation fields: `imageUrl` and publish `date`
- Engagement metrics: `likes`
- Operational timestamps: automatic `createdAt` and `updatedAt`

Near-term schema improvements can include slugs, moderation status, reading time, external source attribution, and indexes for category/date/search queries.

## Backend Workflow Organization

1. **Route definition:** Add or update an endpoint in `backend/routes/`.
2. **Controller logic:** Keep request normalization, validation, and response formatting in `backend/controllers/`.
3. **Persistence:** Add schema fields, indexes, or new collections in `backend/models/`.
4. **Middleware:** Put cross-cutting behavior such as auth, logging, rate limiting, and error handling in `backend/middleware/`.
5. **Configuration:** Use environment variables for secrets and deployment-specific settings.
6. **Verification:** Run syntax checks and API smoke tests before submitting changes.

## Real-Time and Future Integration Roadmap

- Add publish-status workflows so posts can move from draft to review to live publishing.
- Introduce Socket.IO or Server-Sent Events for live newsroom updates and breaking-news alerts.
- Add scheduled ingestion jobs for RSS feeds, trusted news APIs, or editorial automation.
- Add MongoDB indexes for category, date, keyword, and text-search performance.
- Add request validation with a schema library before data reaches controllers.
- Add automated tests for controllers, routes, and database error handling.

## Environment Variables

| Variable | Required | Purpose |
| --- | --- | --- |
| `PORT` | No | Local server port, defaulting to `5000`. |
| `MONGO_URI` | Yes for post APIs | MongoDB connection string. |
| `CLIENT_ORIGIN` | No | Comma-separated list of allowed frontend origins. |
| `NODE_ENV` | No | Controls production-safe error output. |

## Contribution Note

This backend plan documents the scalable direction for Infozap and recognizes the requested backend contribution from [@chamanvashishth](https://github.com/chamanvashishth). It is intended to support maintainers during review and provide a clear path for future backend pull requests.
