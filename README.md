<div align="center">
  <img src="https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/sparkles.svg" width="60" alt="Lumina AI Logo" />
  <h1>✨ Lumina AI</h1>
  <p><strong>Illuminating insights from your personal knowledge base.</strong></p>
  <p>
    A stunning, full-stack Agentic RAG (Retrieval-Augmented Generation) application featuring a premium Glassmorphic Dark Mode UI. Upload PDF documents and interact with them seamlessly using an intelligent AI agent.
  </p>
</div>

---

## 🚀 Features

- 🎨 **Premium Aesthetic**: Gorgeous, sleek dark mode UI with glassmorphism, fluid typography, and vibrant fuchsia/indigo gradients.
- 🧠 **Agentic Chat**: A smart ReAct agent powered by OpenAI GPT-4o that autonomously decides when to query the knowledge base to answer your questions.
- 📚 **PDF Ingestion**: Easily drag-and-drop or upload PDF files to process and embed them directly into the vector database.
- 💬 **Contextual Memory**: The assistant remembers the conversation history for seamless follow-up questions.
- 🔍 **High-Performance Retrieval**: Uses Pinecone vector database and optimized embedding models for lightning-fast semantic search.
- 📊 **Observability**: Built-in LangSmith integration for tracing, monitoring, and debugging agent behavior.

## 🏗️ Architecture

### Frontend (React + Vite)
- **UI Framework**: React built with Vite for ultra-fast HMR and optimized production bundles.
- **Styling**: Custom CSS featuring modern CSS variables, `backdrop-filter` for frosted glass effects, and animated gradients.
- **Typography**: Integrates Google Fonts (`Inter` & `Outfit`) for crisp, modern readability.
- **Interactions**: Real-time markdown rendering (`react-markdown`) and auto-scrolling chat history.

### Backend (Node.js + Express)
- **Server**: Express.js REST API handling CORS, multipart file uploads (`multer`), and chat endpoints.
- **AI Agent**: LangChain ReAct agent orchestrating the reasoning and action loops.
- **Vector Storage**: Pinecone integrated for storing document chunks and performing similarity queries.
- **Data Processing**: LangChain `PDFLoader` and recursive character text splitters for robust document parsing.

## 📋 Prerequisites

Before you begin, ensure you have the following installed and set up:
- **Node.js**: v18 or higher
- **Package Manager**: `npm` or `yarn`
- **Pinecone Account**: You need a free or paid Pinecone account with a provisioned index.
- **OpenAI API Key**: For the GPT-4o LLM.
- **LangSmith Account**: (Optional) For detailed tracing of the agent's thought process.

## 🛠️ Setup Guide

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd agentic-RAG
   ```

2. **Install all dependencies**
   ```bash
   # This will concurrently install dependencies for both the root, server, and client components.
   npm run install:all
   ```

3. **Configure Environment Variables**
   ```bash
   cp .env.example .env
   ```
   Open the `.env` file and populate it with your keys:
   ```env
   # LLM
   OPENAI_API_KEY=your_openai_api_key
   
   # Vector Database
   PINECONE_API_KEY=your_pinecone_api_key
   PINECONE_INDEX=your_pinecone_index_name
   
   # Optional: LangSmith Tracing
   LANGSMITH_TRACING=true
   LANGSMITH_ENDPOINT=https://api.smith.langchain.com
   LANGSMITH_API_KEY=your_langsmith_key
   LANGSMITH_PROJECT="Lumina AI"
   ```

## 🚀 Running the Application

Launch the entire stack (both frontend and backend) with a single command:

```bash
npm run dev
```

This will concurrently start:
- **Backend API**: `localhost:3001`
- **Frontend App**: `localhost:5173`

Open your browser to the frontend URL to experience Lumina AI.

*If you need to run them individually:*
```bash
npm run dev:server  # Starts only the Node.js backend
npm run dev:client  # Starts only the React frontend
```

## 🔄 How It Works

1. **Ingestion Pipeline (`/api/ingest`)**:
   - You upload a PDF. `multer` receives it in memory.
   - The document is parsed, its text extracted, and then split into highly contextual chunks (1000 chars w/ 200 overlap).
   - These chunks are embedded and synchronized into your Pinecone index.
2. **Chat Lifecycle (`/api/chat`)**:
   - You ask a question. The Express server passes the query down to the LangChain Agent.
   - The Agent analyzes the prompt. If it identifies that it needs context from your uploaded docs, it triggers the custom `Search Knowledge Base` tool.
   - The vector DB returns semantically relevant chunks. The Agent synthesizes this data and returns a cohesive response to the UI.

## 🐛 Troubleshooting

- **Upload Fails / Connection Refused**: Ensure the backend server is running on port `3001` explicitly. Check for port collisions.
- **Pinecone 401/403 Errors**: Double-check your `PINECONE_API_KEY` and ensure the `PINECONE_INDEX` matches *exactly* what is on your Pinecone dashboard.
- **Vite Port Conflicts**: If port 5173 is busy, Vite will automatically assign 5174. Check your terminal output.

## 📄 License

This project is licensed under the MIT License.
