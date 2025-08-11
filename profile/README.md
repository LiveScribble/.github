# 🚧 LiveScribble (Work In Progress) 🚧

> **Note:** LiveScribble is currently under active development.  

---

**LiveScribble** is a lightweight, real-time collaborative document editor with **live cursor tracking** and **share-by-link editing**.  
It’s built with:

- **Frontend:** [Dioxus](https://dioxuslabs.com/) (Rust → WebAssembly) + [Yrs](https://github.com/y-crdt/y-crdt) CRDT for conflict-free editing.
- **Backend:** Go, Rest API with Gin, WebSocket relay using [Gorilla WebSocket](https://github.com/gorilla/websocket).
- **Database:** PostgreSQL for document snapshots.

## ✨ Features

- **Real-time collaboration** — every keystroke appears instantly for all participants.
- **Conflict-free editing** — powered by Yrs (CRDT).
- **Live presence** — see other users' cursors, selections, and names.
- **Share-by-access** — Grant Access to Others for collaborative editing
- **Offline-safe** — local-first architecture; edits are merged even if the server briefly disconnects.
- **Scalable** — horizontal scaling with Redis Pub/Sub for multi-node setups.

## 🏗 How It Works

LiveScribble uses a **frontend-first CRDT model**:

1. **User opens link** → Browser loads the latest snapshot from the server.
2. **Local edits** are applied instantly in the browser via Yrs CRDT.
3. **CRDT updates** (binary diffs) are sent to the Go server over WebSocket.
4. **Server broadcasts** the diffs to all other connected clients in the same room.
5. **Presence updates** (cursor position, selection, name, color) are sent as JSON and broadcast to others.
6. **Snapshots** are periodically saved to PostgreSQL so the document can be restored later.



