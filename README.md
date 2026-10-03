# ContextGPT (Frontend)

*Note: This project repository was originally initialized as `CryptoAI`, but has been rebranded to ContextGPT.*

ContextGPT is an enterprise-grade B2B internal knowledge base AI. This frontend provides a secure, seamless conversational interface for employees to query company data, technical documentation, and operational context using a customized RAG (Retrieval-Augmented Generation) backend.

## ✨ Key Features

*   **Premium Chat Interface:** A modern, responsive chat UI designed for enterprise AI interactions.
*   **Secure OTP Authentication:** Passwordless/OTP-based login, signup, and password reset flows.
*   **JWT Session Management:** Secure token handling via `localStorage` with automated token injection for API requests.
*   **Sliding Window Memory:** Automatically stores the last 5 chat messages in browser memory to provide continuous conversational context without overloading the LLM context window.
*   **Protected Routing:** Strict route guards separating public authentication pages from the internal RAG chatbot.

## 🛠️ Tech Stack

*   **Framework:** React 18 + TypeScript + Vite
*   **Styling:** Tailwind CSS
*   **Backend:** FastAPI + MongoDB + Mongo Vector Search
*   **LLM:** Gemini-3.5-flash-lite  

## 🚀 Getting Started

### 1. Installation
Ensure you have Node.js installed, then install the dependencies:
```bash
npm install

```

### 2. Environment Variables

Copy the example environment file and configure your backend API URL.

```bash
cp .env.example .env

```

Update your `.env` file to point to your FastAPI backend:

```env
# Example .env configuration
VITE_API_BASE_URL=[http://18.61.252.253:8000](http://18.61.252.253:8000)
# Note: If deploying to production/Cloudflare, update this to your HTTPS domain

```

### 3. Development Server

Start the Vite development server:

```bash
npm run dev

```

## 📂 Architecture & File Structure

The project follows a modular, feature-based architecture:

* **`/src/api/`**: Axios/Fetch wrappers for backend communication (`client.ts`). Maps exactly to the FastAPI backend endpoints for auth and RAG chat.
* **`/src/components/`**: Reusable UI components.
* `chat/`: Chatbot specific UI (Bubbles, Composer, Typing Indicators).
* `common/`: Buttons, Inputs, Spinners, and Toasts.
* `layout/`: Sidebar, Topbar, and standard page wrappers.


* **`/src/context/`**: Global state providers for user authentication sessions and active chat state.
* **`/src/hooks/`**: Custom React hooks. `useChatMemory.ts` handles the logic for storing and rotating the 5-message local storage limit.
* **`/src/pages/`**: High-level page views (`Login`, `Chat`, `Profile`, etc.).
* **`/src/routes/`**: Route wrapper components (`ProtectedRoute`, `PublicRoute`) that intercept navigation based on JWT presence.
* **`/src/services/`**: Pure TypeScript utility services handling `localStorage` interactions (`authStorage.ts` for JWTs, `chatMemory.ts` for message history).

## 🧠 Local Chat Memory System

To optimize token usage and maintain privacy, the frontend implements a local sliding-window memory system (`/src/services/chatMemory.ts`).

1. When a user sends a message, it is appended to `localStorage`.
2. If the history exceeds **5 messages**, the oldest message is automatically shifted out.
3. On page reload, `useChatMemory` rehydrates the chat interface from the browser's storage.

## 📦 Build for Production

To generate a production-ready build:

```bash
npm run build

```

The optimized static files will be generated in the `dist/` directory, ready to be deployed to Vercel, Cloudflare Pages, or AWS S3.

```

```
