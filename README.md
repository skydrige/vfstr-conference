# VFSTR Video Conferencing Project

This project implements an intranet-based video conferencing solution with real-time communication using WebRTC. It is designed to work within a university network, providing a low-latency, scalable, and secure video conferencing experience for classrooms, faculty, and students.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Tech Stack](#tech-stack)
- [Directory Structure](#directory-structure)
- [Setup Instructions](#setup-instructions)
- [Client Setup](#client-setup)
- [Server Setup](#server-setup)
- [Deployment](#deployment)
- [Features](#features)
- [Contributing](#contributing)
- [License](#license)

---

## Project Overview

This project is a video conferencing application designed to support multiple peers in a 2-way communication conference. The solution includes:

- **WebRTC** for real-time communication.
- **Node.js** with **Socket.IO** for signaling.
- **Mediasoup** or **Jitsi Videobridge** as the SFU (Selective Forwarding Unit) for media routing.
- **Coturn** for NAT traversal.
- **PostgreSQL** for data storage and **Redis** for session management.
- **React.js** for the client-side user interface.

The system is designed to be deployed and used within a university's intranet environment, ensuring low-latency, high reliability, and scalability.

---

## Tech Stack

### Client-Side
- **React.js**: Frontend framework for building interactive user interfaces.
- **Tailwind CSS**: Utility-first CSS framework for fast, responsive styling.
- **WebRTC API**: Peer-to-peer communication for real-time audio and video calls.
- **Socket.IO**: Real-time signaling for establishing WebRTC connections.

### Server-Side
- **Node.js**: JavaScript runtime for building scalable applications.
- **Express.js**: Minimal and flexible Node.js web application framework.
- **Socket.IO**: Real-time web socket communication for signaling.
- **PostgreSQL**: Relational database for storing user data, room details, and logs.
- **Redis**: In-memory database for caching session data.
- **Mediasoup / Jitsi**: SFU for routing media in large conferences.
- **Coturn**: TURN/STUN server for NAT traversal in WebRTC.

### Development & Deployment
- **Docker**: Containerization for seamless deployment.
- **Kubernetes**: Orchestrates containers for scalability and reliability.
- **Prometheus**: Monitoring system for performance tracking.
- **Grafana**: Visualization tool for monitoring metrics.
- **ELK Stack**: Elasticsearch, Logstash, and Kibana for logging and log analysis.

---

## Directory Structure

```
client/
├── public/                     # Static assets (favicon, index.html, etc.)
├── src/
│   ├── assets/                 # Images, fonts, icons
│   ├── components/             # Reusable components (e.g., VideoPlayer, ChatBox)
│   ├── pages/                  # Page-level components (e.g., Login, Dashboard)
│   ├── context/                # React Context for state management (Auth, Theme)
│   ├── hooks/                  # Custom hooks (useWebRTC, useAuth)
│   ├── services/               # API calls (Axios instance, Signal API)
│   ├── utils/                  # Helper functions (e.g., validators, formatters)
│   ├── App.js                  # Root component
│   ├── index.js                # Entry point
│   ├── routes.js               # Route configurations
├── tailwind.config.js          # Tailwind CSS configuration
├── package.json                # Dependencies and scripts
└── .env                        # Environment variables

server/
├── src/
│   ├── config/                 # Configuration files (DB, environment, constants)
│   ├── controllers/            # Logic for API routes (e.g., UserController, RoomController)
│   ├── models/                 # Database models (e.g., User, Room)
│   ├── routes/                 # API route definitions (e.g., userRoutes, roomRoutes)
│   ├── services/               # Business logic (e.g., signaling logic, token management)
│   ├── utils/                  # Helper utilities (e.g., logger, error handler)
│   ├── middleware/             # Middleware (e.g., auth, validation)
│   ├── index.js                # Main entry point
│   ├── socket.js               # WebSocket signaling logic (using Socket.IO)
│   ├── mediaserver.js          # SFU/Media server integration logic
├── tests/                      # Unit and integration tests
├── package.json                # Dependencies and scripts
├── Dockerfile                  # Docker configuration for the server
└── .env                        # Environment variables
```

---

## Setup Instructions

### Prerequisites
Before setting up the project, make sure you have the following installed:
- **Node.js** (v14.x or later)
- **npm** (v6.x or later)
- **Docker** (for containerization)
- **Docker Compose** (for running multi-container applications)
- **PostgresSQL** and **Redis** (or use Docker containers for both)

### Client Setup

1. **Clone the repository**:
   ```bash
   git clone <repository-url> client
   cd client
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Configure environment variables**:
   Create a `.env` file in the root of the `client` directory and set the API URLs:
   ```env
   REACT_APP_API_URL=http://<server-ip>:<port>/api
   REACT_APP_SOCKET_URL=http://<server-ip>:<port>
   ```

4. **Start the development server**:
   ```bash
   npm start
   ```

5. Open `http://localhost:3000` to view the client in action.

---

### Server Setup

1. **Clone the repository**:
   ```bash
   git clone <repository-url> server
   cd server
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Configure environment variables**:
   Create a `.env` file in the root of the `server` directory and set the following:
   ```env
   DB_HOST=localhost
   DB_PORT=5432
   DB_USER=your_user
   DB_PASSWORD=your_password
   JWT_SECRET=your_secret
   REDIS_HOST=localhost
   REDIS_PORT=6379
   TURN_SERVER=turn:<turn-server-ip>
   TURN_USERNAME=your_turn_user
   TURN_PASSWORD=your_turn_password
   ```

4. **Run the server**:
   ```bash
   npm run dev
   ```

5. The server will be running at `http://localhost:5000`.

---

## Deployment

### Dockerize the Application

1. **Dockerize the Client**:
   - Build the React client into a production bundle:
     ```bash
     npm run build
     ```
   - Create a Docker image and run it:
     ```bash
     docker build -t video-conferencing-client .
     docker run -p 80:80 video-conferencing-client
     ```

2. **Dockerize the Server**:
   - Build the Node.js backend into a Docker image:
     ```bash
     docker build -t video-conferencing-server .
     docker run -p 5000:5000 video-conferencing-server
     ```

3. Use **Docker Compose** to link the client, server, PostgreSQL, Redis, and TURN server for a unified local setup.

---

## Features

- **Real-time Video Conferencing**: Multiple users can join a conference room and communicate via video/audio.
- **WebRTC**: Peer-to-peer communication with minimal latency.
- **Scalable**: Media servers (Mediasoup, Jitsi) ensure scalability for larger conferences.
- **Secure Authentication**: JWT-based authentication for session security.
- **Room Management**: Create, join, and manage video conference rooms.
- **NAT Traversal**: TURN servers facilitate connections behind firewalls.

---

## Contributing

We welcome contributions to this project! If you'd like to contribute, please follow these steps:

1. Fork the repository.
2. Create a new branch for your changes.
3. Make your changes.
4. Commit your changes.
5. Open a pull request.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
