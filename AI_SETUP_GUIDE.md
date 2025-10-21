# AI Assistant Setup Guide

This guide will help you set up the AI-powered chatbot for your portfolio.

## Overview

Your portfolio now includes a RAG (Retrieval Augmented Generation) based AI assistant that:
- Uses OpenAI embeddings to understand your knowledge base
- Performs semantic search to find relevant information
- Generates contextual responses using GPT-4 Turbo
- Provides conversational chat experience for visitors

## Architecture

```
Frontend (React/Vite) → Backend API (Express) → OpenAI API
                              ↓
                        Embeddings (Vector Search)
```

## Setup Steps

### 1. Create Environment File

Create a `.env` file in the project root with your OpenAI API key:

```env
OPENAI_API_KEY=your_openai_api_key_here
PORT=3001
```

### 2. Install Dependencies

```bash
npm install
```

This installs:
- `openai` - OpenAI API client
- `express` - Backend server
- `cors` - Cross-origin resource sharing
- `dotenv` - Environment variable management
- `react-markdown` - Markdown rendering for AI responses
- `remark-gfm` - GitHub Flavored Markdown support
- `rehype-raw` - HTML in markdown support

### 3. Generate Embeddings

Run the embedding generation script to create vector representations of your knowledge base:

```bash
npm run generate-embeddings
```

This will:
- Read all entries from `data/knowledge.json`
- Generate embeddings using OpenAI's `text-embedding-3-small` model
- Save embeddings to `data/embeddings.json`
- Takes ~30 seconds for 25+ entries

**Expected output:**
```
🚀 Starting embedding generation...
📚 Loaded 25 knowledge entries
Processing 1/25: bio-01...
✓ Generated embedding (1536 dimensions)
...
✨ Successfully generated and saved 25 embeddings!
```

### 4. Start the Application

You have two options:

#### Option A: Run Both Servers (Recommended)

```bash
npm run dev:all
```

This runs both:
- Frontend on `http://localhost:5173`
- Backend API on `http://localhost:3001`

#### Option B: Run Separately

Terminal 1 - Frontend:
```bash
npm run dev
```

Terminal 2 - Backend:
```bash
npm run server
```

## File Structure

```
portfolio/
├── data/
│   ├── knowledge.json          # Your knowledge base (source)
│   └── embeddings.json         # Generated embeddings (auto-created)
├── scripts/
│   └── generateEmbeddings.js   # Embedding generation script
├── server/
│   └── index.js                # Express backend API
├── src/
│   └── components/
│       └── ChatWidget.jsx      # Updated chat UI with AI integration
├── .env                        # Environment variables (create this!)
└── package.json                # Updated with new scripts & dependencies
```

## API Endpoints

### POST `/api/chat`
Send a message and get AI response

**Request:**
```json
{
  "message": "Tell me about Omar's projects",
  "conversationHistory": [
    { "role": "user", "content": "previous message" },
    { "role": "assistant", "content": "previous response" }
  ]
}
```

**Response:**
```json
{
  "reply": "Omar has built several impressive projects...",
  "relevantContext": [
    { "id": "project-01", "topic": "project" },
    { "id": "project-02", "topic": "project" }
  ]
}
```

### GET `/api/health`
Check server status

**Response:**
```json
{
  "status": "ok",
  "embeddings": 25,
  "timestamp": "2024-10-10T12:00:00.000Z"
}
```

## How It Works

1. **User sends a message** → Frontend sends to `/api/chat`
2. **Backend generates query embedding** → Converts message to vector
3. **Semantic search** → Finds 3 most relevant knowledge entries using cosine similarity
4. **Context building** → Combines relevant knowledge into system prompt
5. **GPT-4 call** → Sends context + conversation history to OpenAI
6. **Response** → Returns AI-generated answer to frontend

## Technology Stack

### Frontend
- React 18
- Vite
- Tailwind CSS
- GSAP animations
- Framer Motion

### Backend
- Node.js
- Express.js
- OpenAI SDK v4

### AI/ML
- OpenAI GPT-4 Turbo
- text-embedding-3-small (1536 dimensions)
- Cosine similarity for vector search

## Customization

### Update Knowledge Base

1. Edit `data/knowledge.json`
2. Re-run `npm run generate-embeddings`
3. Restart backend server

### Change AI Model

In `server/index.js`, update:
```javascript
model: 'gpt-4-turbo-preview'  // or 'gpt-3.5-turbo', 'gpt-4', etc.
```

### Adjust Context Size

In `server/index.js`, change `topK` parameter:
```javascript
const relevantContext = findRelevantContext(
  queryEmbedding.data[0].embedding,
  5  // Get top 5 results instead of 3
);
```

### Modify System Prompt

Edit the system message in `server/index.js` to change AI personality/behavior.

## Costs

Approximate costs per 1000 requests:

- **Embeddings (one-time):** $0.02 for 25 entries
- **GPT-4 Turbo:** ~$0.30-0.50 per 1000 messages
- **Query embeddings:** $0.02 per 1000 queries

**Total: ~$0.35 per 1000 conversations**

## Troubleshooting

### "Failed to get response"
- Ensure backend is running on port 3001
- Check CORS is enabled
- Verify OpenAI API key is valid

### "Failed to load embeddings"
- Run `npm run generate-embeddings` first
- Check `data/embeddings.json` exists

### High latency
- Use `gpt-3.5-turbo` instead of GPT-4
- Reduce `topK` context size
- Implement caching for common questions

## Production Deployment

### Backend Options
1. **Vercel/Netlify Functions** - Serverless
2. **Railway/Render** - Traditional hosting
3. **AWS Lambda** - Serverless

### Environment Variables
Remember to set `OPENAI_API_KEY` in production environment!

### Security
- Never commit `.env` file (already in `.gitignore`)
- Use environment variables in production
- Consider rate limiting for API endpoints
- Implement CORS whitelist in production

## Next Steps

- ✅ Set up `.env` file
- ✅ Install dependencies
- ⏳ Generate embeddings
- ⏳ Test locally
- ⏳ Deploy to production

## Support

If you encounter issues:
1. Check console logs (both frontend and backend)
2. Verify API key is valid
3. Ensure ports 5173 and 3001 are available
4. Check network tab in browser DevTools

---

Enjoy your AI-powered portfolio! 🚀✨

