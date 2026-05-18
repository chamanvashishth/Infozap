# 📰 Infozap — Powerful Current Affairs Ecosystem

![Version](https://img.shields.io/badge/Version-1.0.0-blue)
![B.Voc IoT](https://img.shields.io/badge/Program-B.Voc_Internet_of_Things-orange)
![Institution](https://img.shields.io/badge/Institute-Dayalbagh_Educational_Institute-darkblue)

**Infozap** is a professional-grade web platform designed to deliver real-time, viral current affairs. Developed as a flagship Web Development project for the **B.Voc (Internet of Things)** program in **2026**, it showcases a seamless integration of modern frontend design and robust backend architecture.

---

## 🎓 Project Context

This platform was built under the academic guidance of **Dayalbagh Educational Institute (DEI)**. It represents the collective effort of the B.Voc (IoT) batch of 2026 to bridge the gap between traditional journalism and automated digital infrastructure.

- **Project Lead & Manager:** Nitesh Chaurasiya
- **Research & Development Team:** B.Voc (IoT) Class of 2026
- **Backend Development Contributor:** [@chamanvashishth](https://github.com/chamanvashishth)

---

## 🚀 Key Features

- **Dynamic News Feed:** Real-time rendering of news cards across categories like AI, IoT, Defence, and Finance.
- **Advanced Compose Editor:** A custom-built editor for content creators to upload posts with hashtags, keywords, and metadata.
- **Responsive Architecture:** Fully optimized for mobile, tablet, and desktop viewing.
- **Category Filtering:** Seamless navigation through a 3-column grid layout for specific news topics.
- **Professional UX:** Implements hollow-outline typography, skeleton loading states, and smooth hover transitions.
- **RESTful Backend Foundation:** Node.js and Express.js API routes support dynamic post creation, listing, category filtering, likes, and health checks.
- **MongoDB-Ready Content Storage:** Mongoose schemas organize articles, categories, discovery metadata, and engagement data for future automation.

---

## 🛠️ Technical Stack

### Frontend

- **HTML5:** Semantic structure for SEO and accessibility.
- **CSS3:** Custom properties, CSS Grid, and Flexbox for modern layouts.
- **JavaScript (Vanilla):** Dynamic DOM manipulation and API integration.

### Backend

- **Node.js:** Server-side runtime for the Infozap API.
- **Express.js:** Lightweight framework for RESTful API routing and middleware composition.
- **MongoDB + Mongoose:** Flexible NoSQL persistence for dynamic news articles.
- **Vercel Serverless Adapter:** `api/[...all].js` exports the Express app for serverless hosting.

---

## 📂 Project Structure

```text
current-affairs-web/
├── api/
│   └── [...all].js              # Serverless adapter for the Express app
├── assets/
│   ├── css/                     # Modular stylesheets (index.css, post.css, etc.)
│   ├── js/                      # Frontend logic (app.js, category.js)
│   └── icons/                   # Favicons and brand assets
├── backend/
│   ├── config/                  # Database connection helpers
│   ├── controllers/             # API request handlers
│   ├── middleware/              # Logger, auth hook, and error handling
│   ├── models/                  # Mongoose schemas
│   ├── routes/                  # RESTful route definitions
│   └── server.js                # Express app configuration
├── docs/
│   └── backend-architecture.md  # Backend architecture and API roadmap
├── index.html                   # Main landing page
├── category.html                # Topic-wise listing
├── post.html                    # Individual article view
├── about.html                   # Project history and credits
└── compose.html                 # Post creation portal
```

---

## 🔌 Backend API Overview

| Method | Endpoint | Description |
| --- | --- | --- |
| `GET` | `/api` | API welcome/status response with core endpoint links. |
| `GET` | `/api/health` | Operational health response for deployment monitoring. |
| `GET` | `/api/posts` | Fetch all dynamic posts from MongoDB. |
| `POST` | `/api/posts` | Create a new news post. |
| `GET` | `/api/posts/:id` | Fetch a post by MongoDB ObjectId. |
| `GET` | `/api/posts/category/:category` | Fetch posts by category. |
| `PATCH` | `/api/posts/:id/like` | Increment a post's like count. |

For backend architecture planning, workflow organization, MongoDB model notes, and future real-time integration plans, see [`docs/backend-architecture.md`](docs/backend-architecture.md).

---

## ⚙️ Backend Environment Variables

| Variable | Required | Purpose |
| --- | --- | --- |
| `PORT` | No | Local server port, defaulting to `5000`. |
| `MONGO_URI` | Yes for post APIs | MongoDB connection string. |
| `CLIENT_ORIGIN` | No | Comma-separated allowed frontend origins. |
| `NODE_ENV` | No | Controls production-safe error output. |

---

## ▶️ Running Locally

```bash
npm install
npm start
```

The API will be available at `http://localhost:5000/api`, and the health check will be available at `http://localhost:5000/api/health`.
