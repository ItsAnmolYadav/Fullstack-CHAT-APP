# ⚡ Z-CHAT

**A high-performance real-time chat engine with hybrid responsive UX**

## Overview

Z-CHAT is a full-stack real-time messaging application built for performance and usability across all devices. It features JWT-based authentication, Cloudinary-powered media uploads, bidirectional WebSocket communication, and a carefully engineered hybrid UX that adapts seamlessly between desktop and mobile workflows — including iOS safe-zone support and virtual keyboard layout handling.


SCREENSHOTS 

SIGN UP PAGE  
<img width="1917" height="989" alt="Screenshot 2026-07-11 223718" src="https://github.com/user-attachments/assets/272d810a-252f-4023-a18c-53296482f0f9" />

HOME PAGE
<img width="1916" height="987" alt="Screenshot 2026-07-11 223744" src="https://github.com/user-attachments/assets/cfdc4b68-4fdc-4808-b708-6c9e796f8fb9" />

CHAT
<img width="1289" height="919" alt="Screenshot 2026-07-11 223826" src="https://github.com/user-attachments/assets/40dbaf99-2d52-41ad-aaf1-52ef2914652b" />

DELETE FEATURES
<img width="886" height="861" alt="Screenshot 2026-07-11 223940" src="https://github.com/user-attachments/assets/3110d343-373c-4162-b779-efd6bdc9901c" />

PROFILE PAGE
<img width="1473" height="932" alt="Screenshot 2026-07-11 223920" src="https://github.com/user-attachments/assets/1444445a-947c-4069-a2f5-a7b1910067b9" />

SETTINGS
<img width="1169" height="937" alt="Screenshot 2026-07-11 223852" src="https://github.com/user-attachments/assets/1fc82e89-b92c-4512-80bd-a0a6cbe46d70" /> 

---

## ✨ Features

### 🔐 Authentication & User Management
- **JWT authentication** stored in HTTP-only cookies for secure, stateless sessions
- **Protected routes** on both frontend (React Router guards) and backend (`protectRoute` middleware)
- **Username availability check** before signup with a dedicated endpoint
- **Profile updates** — change display name, username, and profile picture
- **Account deletion** with full data cleanup

### 💬 Messaging
- **Real-time messaging** over WebSockets with automatic long-polling fallback
- **Image support** — send photos via Cloudinary CDN (10MB upload limit)
- **Edit & delete for everyone** — changes propagate instantly to all connected clients
- **Delete for me** — client-side cascade with no server-side side effects
- **Delete conversation** — clear an entire chat with a specific user
- **Clear all chats** — wipe all conversations at once

### ⚡ Real-Time Presence
- **Online user tracking** — see who's currently active via Socket.io room management
- **Instant delivery** — messages emit and render without page refresh

### 🎨 UI & UX
- **32 DaisyUI themes** — user-selectable from the Settings page, persisted via Zustand
- **Optimistic UI updates** — messages appear instantly before server confirmation; rolled back gracefully on failure
- **Auto-sizing message input** — scales up to `120px` dynamically based on content, no cramped typing
- **Enter-to-send** limited to viewports wider than `768px`, matching standard mobile keyboard behavior
- **Dynamic layout retention** using `h-[100dvh]` — prevents layout shifting when mobile virtual keyboards appear
- **iOS safe-zone support** via native inset padding to prevent gesture bars from overlapping UI

### ⚙️ Engineering
- **Monorepo structure** — shared frontend + backend served from a single Express server in production
- **ESM throughout** — both frontend (Vite) and backend use ES Modules (`"type": "module"`)
- **Catch-all SPA routing** — Express serves `index.html` for all non-API routes in production

---

## 🛠 Tech Stack

### Frontend

| Package | Version | Purpose |
|---|---|---|
| `react` | 19 | UI library |
| `react-router-dom` | 7 | Client-side routing & route guards |
| `zustand` | 5 | Global state (auth, theme, chat) |
| `socket.io-client` | 4.8 | Real-time WebSocket client |
| `axios` | 1.x | HTTP client for REST API calls |
| `tailwindcss` + `daisyui` | 4 / 5 | Utility-first styling + theming |
| `lucide-react` | 0.5x | Icon library |
| `react-hot-toast` | 2.x | Toast notifications |
| `vite` | 7 | Build tool & dev server |

### Backend

| Package | Version | Purpose |
|---|---|---|
| `express` | 5 | HTTP server & REST API |
| `socket.io` | 4.8 | WebSocket server |
| `mongoose` | 9 | MongoDB ODM |
| `jsonwebtoken` | 9 | JWT generation & verification |
| `bcryptjs` | 3 | Password hashing |
| `cloudinary` | 2 | Image upload & CDN |
| `cookie-parser` | 1.4 | HTTP-only cookie parsing |
| `cors` | 2.8 | Cross-origin request handling |
| `dotenv` | 17 | Environment variable loading |
| `nodemon` | 3 | Dev server auto-restart |

---

## 📂 Project Structure

```
z-chat/
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Navbar.jsx
│   │   │   ├── ChatContainer.jsx      # Message queue coordinator & real-time sync
│   │   │   └── MessageInput.jsx       # Input capture, auto-resize, file encoding
│   │   ├── pages/
│   │   │   ├── HomePage.jsx
│   │   │   ├── LoginPage.jsx
│   │   │   ├── SignUpPage.jsx
│   │   │   ├── SettingsPage.jsx       # Theme selection (32 DaisyUI themes)
│   │   │   └── ProfilePage.jsx
│   │   ├── store/
│   │   │   ├── useAuthStore.js        # Auth state + checkAuth + online users
│   │   │   └── useThemeStore.js       # Theme persistence
│   │   └── App.jsx                    # Route definitions & auth guards
│   ├── package.json
│   └── vite.config.js
│
└── backend/
    └── src/
        ├── controllers/
        │   ├── auth.controller.js     # signup, login, logout, updateProfile, deleteAccount
        │   └── message.controller.js  # getMessages, sendMessage, deleteConversation, clearAllChats
        ├── routes/
        │   ├── auth.route.js          # /api/auth/*
        │   └── message.route.js       # /api/messages/*
        ├── middleware/
        │   └── auth.middleware.js     # protectRoute (JWT verification)
        ├── lib/
        │   ├── db.js                  # MongoDB connection
        │   └── socket.js              # Socket.io server + online user map
        └── index.js                   # App entry point
```

---

## 🚀 Getting Started

### Prerequisites

- **Node.js** `v18+`
- **MongoDB** — local instance or [MongoDB Atlas](https://www.mongodb.com/atlas)
- **Cloudinary** account — [free tier](https://cloudinary.com/) is sufficient

### 1. Clone the repository

```bash
git clone https://github.com/Anmol1578/Z-CHAT.git
cd Z-CHAT
```

### 2. Install dependencies

```bash
# Frontend
cd frontend && npm install

# Backend
cd ../backend && npm install
```

### 3. Configure environment variables

Create a `.env` file inside the `backend/` directory:

```env
# Server
PORT=5001
NODE_ENV=development

# Database
MONGODB_URI=your_mongodb_connection_string

# Auth
JWT_SECRET=your_jwt_secret_key

# Cloudinary (for image uploads)
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# CORS
CLIENT_URL=http://localhost:5173
```

### 4. Run the development servers

```bash
# Terminal 1 — Backend (from /backend)
npm run dev       # runs: nodemon src/index.js

# Terminal 2 — Frontend (from /frontend)
npm run dev       # runs: vite
```

| Service | URL |
|---|---|
| Frontend | `http://localhost:5173` |
| Backend API | `http://localhost:5001` |

### 5. Production build

```bash
# Build the frontend
cd frontend && npm run build

# Serve everything from the backend
cd ../backend && npm start
```

In production, Express serves the compiled frontend from `../frontend/dist` and handles SPA routing with a catch-all `index.html` fallback.

---

## 📡 API Reference

All routes are prefixed with `/api`. Protected routes require a valid JWT cookie.

### Auth — `/api/auth`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `POST` | `/signup` | ❌ | Register a new user |
| `POST` | `/login` | ❌ | Log in and receive JWT cookie |
| `POST` | `/logout` | ❌ | Clear session cookie |
| `GET` | `/check-username/:username` | ❌ | Check username availability |
| `GET` | `/check` | ✅ | Verify current session |
| `PUT` | `/update-profile` | ✅ | Update name, username, or avatar |
| `DELETE` | `/delete-account` | ✅ | Permanently delete account |

### Messages — `/api/messages`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `GET` | `/users` | ✅ | Get all users for the sidebar (excludes self) |
| `GET` | `/:id` | ✅ | Get conversation with a specific user |
| `POST` | `/send/:id` | ✅ | Send a message (text or image) to a user |
| `DELETE` | `/conversation/:id` | ✅ | Delete all messages with a specific user |
| `DELETE` | `/clear` | ✅ | Clear all conversations for the logged-in user |

---

## 🔌 WebSocket Events

The Socket.io server tracks connected users by `userId` and broadcasts events to targeted recipients.

### Outbound (Client → Server)

| Event | Payload | Description |
|---|---|---|
| `editMessage` | `{ messageId, newText, receiverId }` | Edit a sent message |
| `deleteForEveryone` | `{ messageId, receiverId }` | Delete a message for both participants |
| `deleteForMe` | `{ messageId, receiverId }` | Remove a message for the sender only |

### Inbound (Server → Client)

| Event | Payload | Description |
|---|---|---|
| `getOnlineUsers` | `string[]` (user IDs) | Emitted on connect/disconnect with current online user list |
| `newMessage` | `Message` | Delivered to recipient when a new message is sent |
| `messageEdited` | `updatedMessage` | Propagates an edit to all participants |
| `messageDeleted` | `{ messageId }` | Triggers cascade UI removal for all participants |

---

## 🤝 Contributing

Contributions are welcome! To get started:

1. Fork the repository
2. Create a feature branch — `git checkout -b feature/your-feature`
3. Commit your changes — `git commit -m 'feat: add your feature'`
4. Push to your branch — `git push origin feature/your-feature`
5. Open a Pull Request

Please ensure your changes work across both desktop and mobile viewports and that the ESLint config passes (`npm run lint` in `/frontend`).

---

## 📄 License

This project is licensed under the **ISC License**. See the [LICENSE] file for details.

---

⭐ Star this repo if you found it useful!
