# PixlMeet

> **A WebRTC-powered video conferencing platform with JWT-based authentication, inspired by Zoom and Google Meet.**

PixlMeet enables secure, real-time video meetings directly in the browser, without additional software. It uses **WebRTC** for peer-to-peer media streaming and **JWT** for secure authentication and authorization.

---

## Table of Contents

1. [Overview](#overview)
2. [Key Features](#key-features)
3. [Tech Stack](#tech-stack)
4. [Repository Structure](#repository-structure)
5. [Getting Started](#getting-started)

   * [Prerequisites](#prerequisites)
   * [Installation](#installation)
   * [Running the Application](#running-the-application)
6. [Environment Variables](#environment-variables)
7. [Architecture](#architecture)
8. [Security Considerations](#security-considerations)
9. [Deployment](#deployment)
10. [Roadmap](#roadmap)
11. [Contributing](#contributing)
12. [License](#license)

---

## Overview

PixlMeet is a browser-based video conferencing web app, designed to be as intuitive as mainstream meeting platforms but lightweight enough for quick deployment. It supports features like room creation/joining, authentication, and seamless video/audio streaming.

## Key Features

* **WebRTC Video/Audio Conferencing** — Direct peer-to-peer media connection for low latency.
* **JWT Authentication** — Secure login and room access control.
* **Room Management** — Create/join meeting rooms with unique IDs or links.
* **Screen Sharing** — Share your screen with participants.
* **Chat Messaging** — Text-based messaging during calls.
* **Mute/Unmute & Video On/Off Controls** — Easy toggle for privacy.
* **Responsive UI** — Works across desktops and mobile browsers.

## Tech Stack

**Frontend:**

* React (with hooks)
* WebRTC API
* WebSockets (Signaling)
* CSS / Tailwind / Styled Components (verify exact)

**Backend:**

* Node.js
* Express.js
* Socket.IO (for signaling)
* JSON Web Token (JWT)
* MongoDB (user data, rooms)

**Other:**

* STUN/TURN servers (for NAT traversal)
* dotenv for environment configuration

## Repository Structure

```
PixlMeet/
├── backend/         # Express server, signaling, authentication
├── frontend/        # React app for UI and WebRTC handling
├── package.json     # Root package scripts (if applicable)
└── README.md
```

## Getting Started

### Prerequisites

* Node.js >= 16
* npm or yarn
* MongoDB (local or cloud)
* A STUN/TURN server configuration (can use public STUN for dev)

### Installation

```bash
git clone https://github.com/silent-knight19/PixlMeet.git
cd PixlMeet

# Backend setup
cd backend
npm install

# Frontend setup
cd ../frontend
npm install
```

### Running the Application

In separate terminals:

```bash
# Start backend
cd backend
npm run dev   # or npm start

# Start frontend
cd ../frontend
npm start
```

The frontend will run on `http://localhost:3000` (CRA) or similar, backend on `http://localhost:5000` by default.

## Environment Variables

Create `.env` files for both frontend and backend.

**Backend `.env`**

```
PORT=5000
MONGO_URI=mongodb://localhost:27017/pixlmeet
JWT_SECRET=your_jwt_secret
CLIENT_URL=http://localhost:3000
STUN_SERVER=stun:stun.l.google.com:19302
TURN_SERVER=turn:your.turn.server:3478
TURN_USERNAME=user
TURN_PASSWORD=pass
```

**Frontend `.env`** (React)

```
REACT_APP_API_URL=http://localhost:5000
REACT_APP_STUN_SERVER=stun:stun.l.google.com:19302
REACT_APP_TURN_SERVER=turn:your.turn.server:3478
```

## Architecture

High-level flow:

```
[User Browser] ⇄ [Frontend React SPA] ⇄ [Backend API + Socket.IO] ⇄ [MongoDB]
          ↘────────── WebRTC (P2P media) ─────────↙
```

1. **Authentication** — User logs in; backend issues JWT.
2. **Signaling** — Socket.IO handles exchanging SDP and ICE candidates between peers.
3. **Media Streaming** — WebRTC establishes peer-to-peer connection for video/audio.
4. **Room Management** — Backend validates room existence and permissions.

## Security Considerations

* JWT secrets must be strong and kept out of version control.
* Always use HTTPS in production for WebRTC.
* TURN servers should be configured with credentials.
* Validate all signaling messages server-side.

## Deployment

* **Frontend:** Host on Netlify, Vercel, or serve from backend.
* **Backend:** Deploy on services like Heroku, Render, DigitalOcean, or AWS EC2.
* **Database:** MongoDB Atlas or self-hosted Mongo.
* **TURN/STUN:** Use a reliable TURN service (e.g., Twilio Network Traversal Service) for production reliability.

## Roadmap

* Add meeting recording feature.
* Implement raise-hand and reactions.
* Improve chat with file/image sharing.
* Enhance UI with participant grid layout.
* Add tests (unit & integration).

## Contributing

1. Fork the repo.
2. Create a feature branch: `git checkout -b feature-name`
3. Commit changes with clear messages.
4. Push branch and open a Pull Request.

## License

This project currently has no license file — consider adding one (MIT, Apache 2.0, etc.)

---

Maintained by [silent-knight19](https://github.com/silent-knight19)
