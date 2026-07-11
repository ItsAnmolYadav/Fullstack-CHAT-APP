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
