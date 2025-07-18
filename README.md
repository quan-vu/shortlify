# 🚀 ShortlinkHQ - OpenSource Shortlink Project

## ✅ Project Overview

### 🔹 Project Name: `ShortlinkHQ`
An open-source, privacy-respecting, scalable shortlink platform inspired by Bitly but built with modern tech.

### 🔹 Objective
Enable users to shorten URLs, track analytics, create branded links, and manage them via a dashboard or API.

---

## 📌 1. Project Definition

| Item             | Description                                                           |
|------------------|-----------------------------------------------------------------------|
| Target Users     | Developers, marketers, product managers, open-source enthusiasts      |
| Features         | URL shortening, redirection, custom aliases, analytics, QR codes      |
| Access Modes     | Web UI, RESTful API                                                   |
| License          | MIT / Apache 2.0                                                      |
| Deployment       | Docker / Kubernetes-ready, self-hosted or cloud deployment            |

---

## ⚠️ 2. Key Challenges

| Challenge                     | Description                                               |
|------------------------------|-----------------------------------------------------------|
| Scalability                  | Handle high traffic and write volume                      |
| Redirection Latency          | Fast redirection in milliseconds                          |
| Unique Alias Generation      | Avoid collisions while keeping codes short                |
| Analytics Overhead           | Track data without blocking user redirect                 |
| Abuse Prevention             | Detect spam or malicious URLs                             |
| Rate Limiting                | Prevent DoS via public APIs                               |
| Multi-region Support         | Efficient global redirects                                |
| User Authentication          | Secure link ownership and management                      |

---

## 🛠️ 3. Solution Design

### 3.1 🔧 Core Features

- ✅ URL Shortening with optional custom aliases
- ✅ Expiration by date or click count
- ✅ QR Code generation
- ✅ Analytics: IP, device, browser, referrer
- ✅ User Dashboard with login
- ✅ API Key for 3rd-party usage
- ✅ Role-based access (admin, user)
- ✅ Spam/Abuse reporting
- ✅ Redirect type (301, 302)

---

### 3.2 🧠 System Design

#### 🔷 Architecture Overview


#### ⚙️ Modules Breakdown

- Auth Module
  JWT-based auth, OAuth2 support, RBAC

- Link Module
  URL validation, alias generation, redirection handling

- Analytics Module
  Background queue to log request data asynchronously

- Admin Module
  Dashboard for managing links and users

- Rate Limiter
  Built-in NestJS guard or Redis-based limiter

#### 🔗 Short URL Flow

1. User submits long URL
2. Server validates and generates alias (or accepts custom one)
3. Stores mapping in PostgreSQL + cache in Redis
4. On redirect:
   - Check Redis cache
   - If not found, query DB
   - Fire background analytics log job
   - Redirect user

### 4. Tech Stack

✅ Backend
- Framework: NestJS
- Database: PostgreSQL (with Prisma ORM)
- Cache: Redis
- Queue (Analytics logging): BullMQ (Redis-backed)
- Rate Limiting: nestjs-rate-limiter, Redis
- Validation: class-validator, zod
- Authentication: JWT / OAuth2 (@nestjs/passport)

✅ Frontend
- React + TailwindCSS
- API calls via Axios
- Charts via Recharts / Chart.js (for analytics)

✅ DevOps
- Docker
- Docker Compose for dev setup
- GitHub Actions for CI/CD
- Helm chart / K8s for cloud deployment

### 📄 5. Database Schema (Simplified)

```sql
users (
  id UUID PK,
  email VARCHAR UNIQUE,
  password_hash TEXT,
  role ENUM('user', 'admin'),
  created_at TIMESTAMP
)

short_links (
  id UUID PK,
  original_url TEXT,
  short_code VARCHAR(10) UNIQUE,
  user_id UUID FK -> users.id,
  click_count INT,
  expires_at TIMESTAMP,
  created_at TIMESTAMP
)

link_clicks (
  id UUID PK,
  short_link_id UUID FK -> short_links.id,
  ip VARCHAR,
  user_agent TEXT,
  referrer TEXT,
  clicked_at TIMESTAMP
)
```

### 🧪 6. Testing Strategy

- Unit tests (Jest) for all modules
- Integration tests for link creation + redirection
- Load testing (k6 or artillery)
- E2E tests for frontend (Playwright)

### 💡 7. Future Enhancements

- [ ] Link preview thumbnails
- [ ] Multi-tenant support
- [ ] Public analytics sharing
- [ ] Geo-targeted redirection
- [ ] Mobile app or PWA
- [ ] Plugin support for analytics, spam detection

### 📢 8. Community & Contribution

- GitHub repository with contribution guide
- Tagged good first issues
- Live demo + deploy in 1 click (Render/Vercel)
- Invite contributors on Discord/Telegram
- Showcase integrations (e.g., browser extension, CLI tool)

