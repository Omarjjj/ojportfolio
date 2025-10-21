# 🚀 Quick Start Guide - AI Portfolio Assistant

Your AI-powered portfolio chat is now ready! Here's how to use it:

## ✅ What's Been Set Up

1. **Environment Configuration** - `.env` file with your OpenAI API key
2. **Knowledge Base** - 19 entries about you in `data/knowledge.json`
3. **Vector Embeddings** - Generated embeddings in `data/embeddings.json` (1536 dimensions each)
4. **Backend API Server** - Express server in `server/index.js`
5. **Updated Chat Widget** - Full AI integration in `src/components/ChatWidget.jsx`

## 🎮 How to Run

### Start Everything (Recommended)
```bash
npm run dev:all
```

This starts:
- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:3001

### Or Start Separately

**Terminal 1 - Frontend:**
```bash
npm run dev
```

**Terminal 2 - Backend:**
```bash
npm run server
```

## 💬 How to Use

1. Open your portfolio at http://localhost:5173
2. Click the floating chat button at the bottom center
3. Ask questions like:
   - "Tell me about Omar's projects"
   - "What are his technical skills?"
   - "Tell me about his recognition"
   - "What is the Multi-University AI Assistant?"
   - "Has Omar done any internships?"

## 🎯 Features

- **Semantic Search**: AI finds relevant information from your knowledge base
- **Contextual Responses**: GPT-4 Turbo generates natural, personalized answers
- **Markdown Formatting**: Beautiful, structured responses with syntax highlighting
  - **Bold** emphasis with glow effects
  - *Italic* technical terms
  - `Code` formatting for technologies
  - Bullet lists with custom arrows
  - Gradient headers with underlines
  - Animated hover effects
- **Conversation Memory**: Keeps track of chat history for context
- **Beautiful UI**: Animated chat widget with GSAP effects
- **Real-time Status**: Shows when AI is thinking
- **Suggested Questions**: Quick start options for visitors
- **Error Handling**: Graceful fallback if backend is offline

## 📊 Stats

- **19 Knowledge Entries** (bio, projects, skills, recognition, etc.)
- **19 Vector Embeddings** (1536 dimensions each)
- **GPT-4 Turbo** powered responses
- **Semantic Search** with cosine similarity
- **Top 3 Context** retrieval for each query

## 🛠️ Commands

| Command | Description |
|---------|-------------|
| `npm run dev` | Start frontend (Vite) |
| `npm run server` | Start backend API |
| `npm run dev:all` | Start both servers |
| `npm run generate-embeddings` | Regenerate embeddings |
| `npm run build` | Build for production |

## 📝 Update Knowledge Base

When you want to add/update information:

1. Edit `data/knowledge.json`
2. Run `npm run generate-embeddings`
3. Restart the backend server

## 🎨 Customize

### Change AI Personality
Edit system prompt in `server/index.js` (line ~69)

### Adjust Context Size
Change `topK` parameter in `server/index.js` (line ~90)
```javascript
findRelevantContext(embedding, 5) // Get 5 instead of 3
```

### Switch AI Model
Update model in `server/index.js` (line ~117)
```javascript
model: 'gpt-3.5-turbo' // Faster & cheaper
// or
model: 'gpt-4-turbo-preview' // Current (best quality)
```

## 🔒 Security

- ✅ `.env` file is in `.gitignore` (API key won't be committed)
- ✅ CORS enabled for local development
- ⚠️ For production: Add CORS whitelist and rate limiting

## 🚀 Next Steps

- [x] Setup complete
- [ ] Test the chat widget
- [ ] Add more knowledge entries
- [ ] Deploy to production
- [ ] Add rate limiting (for production)
- [ ] Consider caching common questions

## 📖 Full Documentation

See `AI_SETUP_GUIDE.md` for detailed information about:
- Architecture overview
- API endpoints
- Costs estimation
- Production deployment
- Troubleshooting

---

**Ready to test!** Just run `npm run dev:all` and open http://localhost:5173 🎉

