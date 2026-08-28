# A.B SaX AI

**Think Smarter. Create Anything.**

A professional, full-featured AI platform with chat, web search, image generation, video creation, file analysis, and more.

## 🌟 Features

- **AI Chat** - Intelligent conversation with streaming responses
- **Web Search** - Real-time internet search with verified sources
- **Image Generation** - Create images from text prompts
- **Video Creation** - Generate AI videos (Pro feature)
- **File Analysis** - Upload and analyze documents
- **Code Mode** - Write and debug code in 15+ languages
- **AI Reasoning** - Advanced reasoning for complex problems
- **Chat History** - Manage conversations
- **User Dashboard** - Track usage and creations

## 📋 Pricing

| Plan | Duration | Price | Features |
|------|----------|-------|----------|
| Free | Lifetime | ₦0 | 5 AI questions |
| Daily | 24h | ₦1,000 | Unlimited |
| Weekly | 7d | ₦7,000 | All features |
| Monthly | 30d | ₦30,000 | All features (POPULAR) |
| Yearly | 365d | ₦100,000 | All features (BEST VALUE) |

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- PostgreSQL 14+

### Installation

```bash
git clone https://github.com/absax1234/ab-sax-ai.git
cd ab-sax-ai
npm install
cp .env.example .env.local
```

### Setup Database

```bash
cd backend
npx prisma migrate dev --name init
```

### Run Development

```bash
# Terminal 1: Frontend
cd frontend
npm run dev

# Terminal 2: Backend
cd backend
npm run dev
```

Visit `http://localhost:3000`

## 📁 Project Structure

```
ab-sax-ai/
├── frontend/          # Next.js application
├── backend/           # Express.js server
├── prisma/            # Database schema
└── docs/              # Documentation
```

## 🔐 Security

- Secure password hashing (bcrypt)
- JWT authentication
- XSS/CSRF protection
- Rate limiting
- Input validation
- File upload security
- Admin authorization

## 💳 Payment System

⚠️ **DEMO ONLY** - No real payments charged

## 📚 Documentation

- [Architecture](./docs/ARCHITECTURE.md)
- [Frontend Setup](./docs/FRONTEND.md)
- [Backend Setup](./docs/BACKEND.md)

## 📄 License

MIT
