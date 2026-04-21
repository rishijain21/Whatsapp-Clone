# 💬 WhatsApp Clone — Full-Stack Real-Time Chat App

<div align="center">

[![Live Demo](https://img.shields.io/badge/🚀_Live_Demo-whatsgram--1dc4e.web.app-25D366?style=for-the-badge)](https://whatsgram-1dc4e.web.app/)
[![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://reactjs.org/)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org/)
[![Socket.io](https://img.shields.io/badge/Socket.io-010101?style=for-the-badge&logo=socketdotio&logoColor=white)](https://socket.io/)
[![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)

**A pixel-faithful WhatsApp Web clone built on the MERN stack with full real-time messaging powered by Socket.io.**

[Live Demo](https://whatsgram-1dc4e.web.app/) · [Report Bug](https://github.com/rishijain21/Whatsapp-Clone/issues) · [View Code](https://github.com/rishijain21/Whatsapp-Clone)

</div>

---

## 🎯 What This Project Demonstrates

This isn't a tutorial-follow-along — it's a production-architecture clone that replicates the core of a world-class messaging product. Building it required solving real engineering challenges:

- **Bidirectional real-time communication** with persistent connections via WebSockets
- **Decoupled microservice-style architecture** — Express API, Socket.io server, and React client are independent processes
- **Live presence tracking** — users' online/offline status is broadcast to relevant peers in real time
- **Auth flows** with secure credential storage and session handling
- **Responsive UI** matching WhatsApp Web's design system using Material-UI

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔐 **User Authentication** | Secure sign-up and login with hashed credentials stored in MongoDB |
| 🔍 **User Search** | Find and start conversations with any registered user |
| ⚡ **Real-Time Messaging** | Instant message delivery via persistent Socket.io connections |
| 🟢 **Online / Offline Status** | Live presence indicators — see when contacts are active |
| ✍️ **Typing Indicators** | "typing..." status shown to the other user in real time |
| 🔔 **Notifications** | In-app alerts for new messages |
| 📱 **Responsive Design** | Adapts to different screen sizes, faithful to WhatsApp Web's layout |

---

## 🏗️ Architecture

This project uses a **3-process architecture** — each concern lives in its own service:

```
┌─────────────────────────────────────────────────────┐
│                     Browser                         │
│              React Client (:3000)                   │
│         (UI, routing, auth state, chat view)        │
└────────────────┬──────────────────┬─────────────────┘
                 │ REST (HTTP)       │ WebSocket
                 ▼                  ▼
   ┌─────────────────────┐  ┌───────────────────────┐
   │   Express Server    │  │   Socket.io Server    │
   │      (:5000)        │  │       (:8900)         │
   │  Auth, users, msgs  │  │  Presence, typing,    │
   │  stored in MongoDB  │  │  message broadcasting │
   └─────────────────────┘  └───────────────────────┘
                 │
                 ▼
        ┌─────────────┐
        │   MongoDB   │
        │  (Atlas DB) │
        └─────────────┘
```

**Why three separate processes?**
- The Socket.io server handles ephemeral, stateful WebSocket connections without polluting the REST API
- The Express server owns all persistent data operations (MongoDB)
- The React client talks to both — REST for data, WebSocket for live events
- This mirrors how production-grade chat systems (Slack, Discord) are structured at a foundational level

---

## 🛠️ Tech Stack

### Frontend
- **React.js** — Component architecture, hooks for state and side-effects
- **Material-UI** — WhatsApp-faithful UI components and theming

### Backend
- **Node.js + Express.js** — REST API for auth, user management, message persistence
- **MongoDB** — Document store for users and chat history
- **Socket.io** — WebSocket server for real-time events (messages, presence, typing)

---

## ⚙️ Local Setup

### Prerequisites
- Node.js v14+
- A MongoDB Atlas account (free tier works)

### 1. Clone the repo

```bash
git clone https://github.com/rishijain21/Whatsapp-Clone.git
cd Whatsapp-Clone
```

### 2. Install dependencies for all three services

```bash
# Express API
cd server && npm install

# React client
cd ../client && npm install

# Socket.io server
cd ../socket && npm install
```

### 3. Configure environment variables

Create a `.env` file inside the `server/` folder:

```env
DB_USERNAME=your_mongodb_username
DB_PASSWORD=your_mongodb_password
```

### 4. Start all three services

Open three terminal windows and run each:

```bash
# Terminal 1 — Express API
cd server && npm start

# Terminal 2 — Socket.io server
cd socket && npm start

# Terminal 3 — React client
cd client && npm start
```

Visit [http://localhost:3000](http://localhost:3000) 🎉

---

## 📁 Project Structure

```
Whatsapp-Clone/
├── client/               # React frontend
│   ├── src/
│   │   ├── components/   # Chat list, message window, sidebar, etc.
│   │   ├── context/      # Auth and socket context providers
│   │   └── pages/        # Login, Register, Home
│   └── package.json
│
├── server/               # Express REST API
│   ├── models/           # Mongoose schemas (User, Message, Conversation)
│   ├── routes/           # Auth, user, message endpoints
│   ├── middleware/        # JWT verification
│   └── package.json
│
└── socket/               # Socket.io real-time server
    ├── index.js          # Connection handling, event broadcasting
    └── package.json
```

---

## 🔮 Potential Enhancements

- [ ] **Group Chats** — Multi-user conversations with group admin controls
- [ ] **Media Sharing** — Send images, videos, and documents (Cloudinary/S3)
- [ ] **Message Read Receipts** — Single ✓ (sent) → Double ✓ (delivered) → Blue ✓✓ (read)
- [ ] **Message Reactions** — Emoji reactions on individual messages
- [ ] **Voice Messages** — Record and send audio clips
- [ ] **End-to-End Encryption** — Implement E2EE for private message security
- [ ] **Push Notifications** — Browser/mobile alerts even when the tab is in the background

---

## 👨‍💻 Developer

**Rishi Jain** — Software Developer at Infosys | B.Tech CSE, SRM Institute Chennai

| Platform | Link |
|---|---|
| 💼 Portfolio | [rishijain21.github.io/rishi-jain](https://rishijain21.github.io/rishi-jain/) |
| 💼 LinkedIn | [linkedin.com/in/rishi-jainn](https://www.linkedin.com/in/rishi-jainn/) |
| 🐙 GitHub | [github.com/rishijain21](https://github.com/rishijain21) |
| 📧 Email | jainnrishii21@gmail.com |

---

<div align="center">

If you found this project useful, consider giving it a ⭐ — it helps a lot!

*Open to collaborations, freelance projects, and full-time opportunities.* 🚀

</div>
