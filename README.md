<h1 align="center">
  <br />
  📚 BookOrbit
  <br />
</h1>

<p align="center">
  <b>A student-to-student book lending ecosystem built for Mansoura University.</b>
  <br />
  <i>Books keep moving. Knowledge keeps growing.</i>
</p>

<p align="center">
  <a href="https://github.com/Qurtuba-Team/BookOrbit-backend">
    <img src="https://img.shields.io/badge/Backend-ASP.NET%20Core%209-512BD4?style=for-the-badge&logo=dotnet&logoColor=white" />
  </a>
  <a href="https://github.com/Qurtuba-Team/BookOrbit-frontend">
    <img src="https://img.shields.io/badge/Frontend-React%2019-61dafb?style=for-the-badge&logo=react&logoColor=black" />
  </a>
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/University-Mansoura-blue?style=for-the-badge" />
</p>

---

## 🎬 Demo

> **📽️ Project Demo Video** → _[https://youtu.be/Vy8LO9UHjMI]_

---

## 📖 What is BookOrbit?

BookOrbit is a campus-exclusive book-sharing platform that lets students at Mansoura University **lend and borrow physical books** from one another — for free. Instead of buying a textbook you'll read once or let it collect dust on a shelf, BookOrbit connects you with a classmate who already has it.

The platform manages the full lifecycle of a book exchange: from student registration and book cataloging, to borrow requests, physical handover confirmation, point settlement, and post-return reviews — all within a trusted, university-verified community.

> **The idea is simple: the more you lend, the more you can borrow.**

---

## 🗂️ Repositories

| Repository | Description | Link |
|:---|:---|:---|
| 📋 **BookOrbit** | Project overview, documentation & planning | *(this repo)* |
| ⚙️ **BookOrbit-backend** | ASP.NET Core 9 REST API — Clean Architecture, DDD, CQRS | [![Backend](https://img.shields.io/badge/Repo-Backend-gray?logo=github)](https://github.com/Qurtuba-Team/BookOrbit-backend) |
| 🎨 **BookOrbit-frontend** | React 19 web app — UI, real-time features, admin panel | [![Frontend](https://img.shields.io/badge/Repo-Frontend-blue?logo=github)](https://github.com/Qurtuba-Team/BookOrbit-frontend) |

--- 

## 📄 Docs

| Document | Description |
|:---|:---|
| [Project Proposal](./Project%20Proposal.pdf) | Original project proposal and scope definition |
| [Presentation](./presentation.pdf) | Project presentation deck |
| [Backend ](https://github.com/Qurtuba-Team/BookOrbit-backend#readme) | Full backend architecture, setup, and developer guide |
| [Frontend ](https://github.com/Qurtuba-Team/BookOrbit-frontend#readme) | Frontend setup and component overview |

---

## 🔥 The Problem

University students spend significant money on textbooks they use for a single semester, only to have them sit unused afterward. Meanwhile, another student a floor above is searching for the exact same book.

- 📈 Textbook prices keep rising
- 🗄️ Students own books they'll never open again
- 🔍 There's no organized way to find books within campus
- 🤝 No trusted system to facilitate exchanges between strangers

---

## ✅ The Solution

BookOrbit turns every student's personal bookshelf into a shared campus resource through:

- **A verified community** — only `@mans.edu.eg` university emails are accepted
- **A trust-based economy** — a points system that rewards reliable lenders and responsible borrowers
- **A structured lifecycle** — from request to handover to return, every step is tracked and confirmed

---

## ⚙️ How It Works

```
  Register (University Email)
        │
        ▼
  Admin Verification
        │
        ▼
  ┌─────────────────────┐
  │   List Your Books   │  →  Browse & Borrow
  └─────────────────────┘
        │
  Send Borrow Request
        │
        ▼
  Owner Reviews & Accepts
        │
        ▼
  Contact Info Exchanged
        │
        ▼
  Physical Handover Confirmed
        │
        ▼
  Active Loan (countdown starts)
        │
        ▼
  Book Returned → Review & Points Settled
```

1. **Register** — Sign up with your official university email (`@mans.edu.eg`).
2. **List** — Add books you're willing to lend with condition details and duration.
3. **Browse** — Search the catalog by title, category, or author.
4. **Request** — Send a borrow request; the owner sees your borrowing history and rating.
5. **Approve** — On acceptance, both sides receive contact information (WhatsApp / Telegram).
6. **Confirm Handover** — Both parties confirm the exchange in-app; the countdown begins.
7. **Return & Review** — Owner confirms return and leaves a review affecting the borrower's reputation.

---

## 🪙 Points Economy

Every student starts with **1 point**, enabling borrowing of one book at a time. Points are the currency of trust on BookOrbit.

| Action | Effect |
|:---|:---|
| Lending a book and receiving a positive review | ➕ Points |
| Returning a book on time and in good condition | ➕ Points |
| Returning a book late or with damage | ➖ Points |
| Confirmed misconduct report by admins | ➖ Points |

More points = more borrowing capacity. The system rewards contribution over pure consumption.

---

## 🏗️ System Architecture

BookOrbit is split into two independent services connected via a REST API.

### High-Level Overview

```
┌─────────────────────────────────────────────────────┐
│                  React 19 Frontend                  │
│   (SPA · React Router 7 · Context API · SignalR)    │
└────────────────────┬────────────────────────────────┘
                     │  HTTPS / REST + WebSocket
┌────────────────────▼────────────────────────────────┐
│            ASP.NET Core 9 REST API                  │
│   (CQRS · Clean Architecture · DDD · JWT Auth)      │
├──────────────────────────────┬──────────────────────┤
│        SQL Server 2022       │  Hybrid Cache         │
│   (EF Core · Identity)       │  (In-Memory + Redis)  │
└──────────────────────────────┴──────────────────────┘
```

### Backend — Clean Architecture

The backend enforces strict dependency inversion across four layered projects:

| Layer | Project | Responsibility |
|:---|:---|:---|
| 🟣 Domain | `BookOrbit.Domain` | Aggregates, Value Objects, Domain Events, Result pattern |
| 🔵 Application | `BookOrbit.Application` | CQRS Handlers, FluentValidation, Pipeline Behaviours |
| 🟠 Infrastructure | `BookOrbit.Infrastructure` | EF Core, Identity, SMTP, Caching, OpenTelemetry |
| 🟢 Presentation | `BookOrbit.Api` | REST Controllers, Middleware, OpenAPI, Rate Limiting |

Key domain aggregates: `Student`, `Book`, `BookCopy`, `LendingListRecord`, `BorrowingRequest`, `BorrowingTransaction`, `PointTransaction`.

### Frontend — React SPA

A modern single-page application with role-based views for students and administrators.

| Layer | Technology |
|:---|:---|
| Framework | React 19, React Router 7 |
| Styling | Tailwind CSS, Framer Motion |
| State Management | Context API, React Hook Form |
| Real-time | SignalR (WebSocket) |
| HTTP | Axios, JWT Auth (Access + Refresh tokens) |

### 📱 Cross-Platform

BookOrbit is designed to run everywhere — the **web app is the primary platform**, with native-feel experiences on both desktop and mobile:

| Platform | Technology | Status |
|:---|:---|:---|
| 🌐 **Web** | React 19 SPA | ✅ Primary platform |
| 🖥️ **Desktop** | Electron (wraps the web app) | ✅ Available |
| 📱 **Mobile** | Capacitor (iOS & Android) | ✅ Available |

---

## 🛡️ Key Technical Features

| Feature | Detail |
|:---|:---|
| **Authentication** | JWT Access Tokens (15 min) + Refresh Token Rotation, HMAC-SHA256 |
| **Authorization** | 16 named policies — role-based, state-based, ownership-based, relationship-based |
| **CQRS** | Every use case as a Command or Query dispatched via MediatR |
| **Observability** | Serilog → Seq · OpenTelemetry → Jaeger · Prometheus → Grafana |
| **Caching** | HybridCache (in-memory + remote) + Output Caching + tag-based invalidation |
| **Rate Limiting** | Three sliding-window policies protecting normal, sensitive, and email endpoints |
| **Error Handling** | `Result<T>` monad + RFC 7807 ProblemDetails — no exception-based flow |
| **Data Safety** | PII masking for logs and API responses (emails, phone numbers, Telegram IDs) |
| **Testing** | Domain unit tests, application unit tests, full subcutaneous integration tests |
| **Containerization** | Docker Compose — 6 services (API, SQL Server, Seq, Prometheus, Grafana, Jaeger) |
| **Real-time UI** | SignalR integration for live notifications |
| **Book Covers** | Automated cover retrieval from Open Library (primary) and Google Books (fallback) |
| **AI Chatbot** | Gemini Pro-powered chatbot for book recommendations and user assistance |

---

## 🔒 Trust & Safety

- Students register only with a verified `@mans.edu.eg` university email.
- Before borrowing, users accept compensation terms covering potential damage or loss.
- Owners can file dispute reports after a return; admins review and adjust points accordingly.
- Real identities are always behind every transaction — no anonymous actors.

---

## 📦 Infrastructure (Docker Compose)

The entire backend stack is orchestrated with Docker Compose:

| Service | Port | Purpose |
|:---|:---|:---|
| BookOrbit API | `7240` | REST API |
| SQL Server 2022 | `1433` | Primary database |
| Seq | `8081` | Structured log viewer |
| Jaeger | `16686` | Distributed tracing UI |
| Prometheus | `9090` | Metrics query engine |
| Grafana | `3000` | Dashboards (metrics + traces) |

---

## 🌿 Features in Progress (Branch-Only)

The following advanced features were **fully implemented in dedicated backend branches** but were **not merged into `main`** due to time constraints and the project deadline. They are complete and ready for integration in a future release.

| Feature | Description |
|:---|:---|
| 🤖 **Recommendation System** | Personalized book recommendations based on borrowing history and student preferences. |
| 🖼️ **AI-Optimized Book Cover Images** | AI pipeline that enhances and corrects book cover images captured by users' cameras. |
| 🔍 **AI-Powered Search** | Semantic, fuzzy search powered by AI — users no longer need to know the exact book title or author name. |
| 💬 **AI Chatbot Integration** | Conversational chatbot to assist users with book discovery, borrowing guidance, and platform navigation. |

---

## 👥 Team

Built by the **Qurtuba Team** — students at Mansoura University.

| Name | Role | GitHub | LinkedIn |
|:---|:---|:---|:---|
| **Adham Eltantawi** | Team Lead | [@adhameltantawi](https://github.com/adhameltantawi) | [LinkedIn](https://www.linkedin.com/in/adhameltantawi/) |
| **Eyad Dawood** | Backend Lead | [@Eyad-Dawood](https://github.com/Eyad-Dawood) | [LinkedIn](https://www.linkedin.com/in/eyad-dawood-845719388/) |
| **Abdelrahman Mohy** | Backend Developer | [@AbdelrahmanMohye0](https://github.com/AbdelrahmanMohye0) | [LinkedIn](https://www.linkedin.com/in/abdelrahmanmohye/) |
| **Abdelrahman Yasser** | Frontend Lead | [@Abdulrahman-Yasser-dev](https://github.com/Abdulrahman-Yasser-dev) | [LinkedIn](https://www.linkedin.com/in/abdulrahman-yasser-dev/) |
| **Omar Ashraf** | Frontend Developer | [@Omar-azmazy](https://github.com/Omar-azmazy) | [LinkedIn](https://www.linkedin.com/in/omarashraf17/) |
| **Abdelrahman Nofal** | Frontend Developer | [@Abdulrhman65](https://github.com/Abdulrhman65) | [LinkedIn](https://www.linkedin.com/in/abdulrhman-nofal-113b96387/) |

---

## 📜 License

MIT License — © 2026 Qurtuba Team

---

<p align="center">
  <i>Built by students, for students — Mansoura University 🎓</i>
</p>
