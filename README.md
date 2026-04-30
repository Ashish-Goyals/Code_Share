# Collaborative Code Editor

A real-time collaborative code editor built with Monaco Editor, Yjs, and Socket.IO. Multiple users can edit the same document simultaneously with live cursor and presence awareness.

## Tech Stack

**Frontend**
- React 19
- Monaco Editor (`@monaco-editor/react`)
- Yjs + `y-monaco` — CRDT-based document sync
- `y-socket.io` — Yjs Socket.IO provider
- Tailwind CSS v4
- Vite

**Backend**
- Node.js + Express
- Socket.IO
- `y-socket.io` server — handles Yjs document sync over WebSockets

## Project Structure

```
docker_aws/
├── backend/
│   ├── server.js        # Express + Socket.IO + YSocketIO server
│   └── package.json
└── frontend/
    ├── src/
    │   ├── app/
    │   │   ├── App.jsx  # Main app component
    │   │   └── App.css
    │   └── main.jsx
    ├── vite.config.js
    └── package.json
```

## Getting Started

### Prerequisites

- Node.js 18+
- npm

### 1. Start the backend

```bash
cd backend
npm install
node server.js
```

Server runs on `http://localhost:3000`.

### 2. Start the frontend

```bash
cd frontend
npm install
npm run dev
```

Frontend runs on `http://localhost:5173`.

### 3. Open in browser

Navigate to `http://localhost:5173?username=yourname` or open the app and enter a username when prompted.

Open the same URL in another tab or browser with a different username to see real-time collaboration.

## How It Works

1. User enters a username — stored in the URL as `?username=`
2. A Yjs document (`Y.Doc`) is created and bound to the Monaco editor via `y-monaco`
3. A `SocketIOProvider` connects to the backend and syncs the Yjs document across all connected clients
4. Awareness (cursor positions, user presence) is shared via `provider.awareness`
5. On refresh, the provider re-syncs the full document state from the server before showing the editor

## API Endpoints

| Method | Path      | Description        |
|--------|-----------|--------------------|
| GET    | `/`       | Health check       |
| GET    | `/health` | Server status      |

## Scripts

**Backend**
```bash
node server.js       # Start server
```

**Frontend**
```bash
npm run dev          # Start dev server
npm run build        # Production build
npm run preview      # Preview production build
npm run lint         # Run ESLint
```
