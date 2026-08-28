# A.B SaX AI - Architecture Documentation

## System Overview

A.B SaX AI is built as a full-stack monorepo application with clear separation between frontend and backend services.

```
┌─────────────────────────────────────────────────────────┐
│                   Client Layer                          │
│         Next.js Frontend (React + Tailwind)             │
└────────────────────┬────────────────────────────────────┘
                     │ HTTP/WebSocket
┌────────��───────────▼────────────────────────────────────┐
│                   API Layer                             │
│         Express.js Backend (Node.js)                    │
│  ┌─────────────────────────────────────────────────┐   │
│  │ Routes & Controllers (API Endpoints)            │   │
│  └──────────────────────┬──────────────────────────┘   │
│  ┌──────────────────────▼──────────────────────────┐   │
│  │ Services & Business Logic                       │   │
│  │ - Auth Service                                  │   │
│  │ - AI Service                                    │   │
│  │ - Search Service                                │   │
│  │ - Image Service                                 │   │
│  │ - Video Service                                 │   │
│  │ - File Service                                  │   │
│  │ - Payment Service                               │   │
│  │ - Usage Service                                 │   │
│  └──────────────────────┬──────────────────────────┘   │
│  ┌──────────────────────▼──────────────────────────┐   │
│  │ Middleware & Utils                              │   │
│  │ - Authentication                                │   │
│  │ - Rate Limiting                                 │   │
│  │ - Error Handling                                │   │
│  │ - Validation                                    │   │
│  └──────────────────────┬──────────────────────────┘   │
└────────────────────┬────────────────────────────────────┘
                     │
        ┌────────────┼────────────┬─────────────┐
        │            │            │             │
        ▼            ▼            ▼             ▼
   PostgreSQL    Redis      External APIs   File Storage
   (Database)   (Cache)     (AI, Search)      (S3)
```

## Frontend Architecture

### Tech Stack
- **Framework**: Next.js 14 (App Router)
- **Styling**: Tailwind CSS + CSS Modules
- **State Management**: Zustand + React Query
- **UI Components**: Radix UI + Custom Components
- **Animation**: Framer Motion
- **Real-time**: Socket.io
- **Forms**: React Hook Form + Zod

### Directory Structure
```
frontend/
├── app/                          # Next.js App Router
│   ├── (auth)/                  # Auth pages group
│   │   ├── login/              # Login page
│   │   ├── signup/             # Signup page
│   │   └── forgot-password/    # Password reset
│   ├── (dashboard)/            # Dashboard pages
│   │   ├── chat/               # Main chat interface
│   │   ├── dashboard/          # User dashboard
│   │   ├── settings/           # Settings page
│   │   └── admin/              # Admin panel
│   ├── layout.tsx              # Root layout
│   ├── page.tsx                # Landing page
│   └── error.tsx               # Error page
├── components/                  # Reusable React components
│   ├── shared/                 # Shared components
│   │   ├── Navbar.tsx
│   │   ├── Sidebar.tsx
│   │   ├── Button.tsx
│   │   └── Modal.tsx
│   ├── chat/                   # Chat-specific components
│   │   ├── ChatMessage.tsx
│   │   ├── ChatInput.tsx
│   │   ├── ChatHistory.tsx
│   │   └── ConversationList.tsx
│   ├── dashboard/              # Dashboard components
│   ├── admin/                  # Admin components
│   └── forms/                  # Form components
├── hooks/                       # Custom React hooks
│   ├── useAuth.ts
│   ├── useChat.ts
│   ├── useUser.ts
│   └── useTheme.ts
├── services/                    # API client services
│   ├── api.ts                  # Axios configuration
│   ├── authService.ts
│   ├── chatService.ts
│   ├── searchService.ts
│   ├── imageService.ts
│   ├── videoService.ts
│   ├── fileService.ts
│   ├── userService.ts
│   └── paymentService.ts
├── stores/                      # Zustand stores
│   ├── authStore.ts
│   ├── chatStore.ts
│   ├── uiStore.ts
│   └── themeStore.ts
├── types/                       # TypeScript types
│   ├── index.ts
│   ├── auth.ts
│   ├── chat.ts
│   ├── user.ts
│   └── api.ts
├── utils/                       # Utility functions
│   ├── format.ts
│   ├── validators.ts
│   ├── constants.ts
│   └── helpers.ts
├── styles/                      # Global styles
│   ├── globals.css
│   └── variables.css
├── public/                      # Static assets
│   ├── images/
│   ├── icons/
│   └── fonts/
├── config/                      # Configuration
│   ├── site.config.ts
│   └── navigation.ts
└── package.json
```

## Backend Architecture

### Tech Stack
- **Runtime**: Node.js 18+
- **Framework**: Express.js
- **Database**: PostgreSQL
- **ORM**: Prisma
- **Authentication**: JWT + bcrypt
- **Validation**: Zod
- **File Upload**: Multer
- **Rate Limiting**: Redis
- **Real-time**: Socket.io

### Directory Structure
```
backend/
├── src/
│   ├── index.ts                # Application entry point
│   ├── app.ts                  # Express app configuration
│   ├── routes/                 # API route handlers
│   │   ├── auth.ts
│   │   ├── chat.ts
│   │   ├── search.ts
│   │   ├── images.ts
│   │   ├── videos.ts
│   │   ├── files.ts
│   │   ├── users.ts
│   │   ├── subscriptions.ts
│   │   ├── payments.ts
│   │   └── admin.ts
│   ├── controllers/            # Request handlers
│   │   ├── authController.ts
│   │   ├── chatController.ts
│   │   ├── searchController.ts
│   │   ├── imageController.ts
│   │   ├── videoController.ts
│   │   ├── fileController.ts
│   │   ├── userController.ts
│   │   ├── subscriptionController.ts
│   │   └── adminController.ts
│   ├── services/               # Business logic
│   │   ├── auth/
│   │   │   ├── authService.ts
│   │   │   ├── passwordService.ts
│   │   │   └── sessionService.ts
│   │   ├── ai/
│   │   │   ├── aiService.ts
│   │   │   ├── providers/
│   │   │   │   ├── openaiProvider.ts
│   │   │   │   ├── anthropicProvider.ts
│   │   │   │   └── deepseekProvider.ts
│   │   │   └── reasoning.ts
│   │   ├── search/
│   │   │   ├── searchService.ts
│   │   │   ├── providers/
│   │   │   │   ├── bingProvider.ts
│   │   │   │   └── googleProvider.ts
│   │   │   └── sourceRetrieval.ts
│   │   ├── image/
│   │   │   ├── imageService.ts
│   │   │   ├── providers/
│   │   │   │   ├── openaiProvider.ts
│   │   │   │   └── stabilityProvider.ts
│   │   │   └── gallery.ts
│   │   ├── video/
│   │   │   ├── videoService.ts
│   │   │   ├── providers/
│   │   │   │   └── synthesiaProvider.ts
│   │   │   └── credits.ts
│   │   ├── file/
│   │   │   ├── fileService.ts
│   │   │   ├── validators.ts
│   │   │   └── storage.ts
│   │   ├── user/
│   │   │   ├── userService.ts
│   │   │   ├── profileService.ts
│   │   │   └── preferencesService.ts
│   │   ├── subscription/
│   │   │   ├── subscriptionService.ts
│   │   │   ├── planService.ts
│   │   │   └── billingService.ts
│   │   ├── payment/
│   │   │   ├── demoPaymentService.ts
│   │   │   └── transactionService.ts
│   │   └── usage/
│   │       ├── usageService.ts
│   │       ├── limiter.ts
│   │       └── tracker.ts
│   ├── middleware/             # Express middleware
│   │   ├── auth.ts
│   │   ├── errorHandler.ts
│   │   ├── rateLimiter.ts
│   │   ├── validation.ts
│   │   ├── cors.ts
│   │   └── logging.ts
│   ├── models/                 # Prisma client (generated)
│   ├── utils/                  # Utility functions
│   │   ├── jwt.ts
│   │   ├── crypto.ts
│   │   ├── validation.ts
│   │   ├── logger.ts
│   │   └── constants.ts
│   ├── config/                 # Configuration
│   │   ├── database.ts
│   │   ├── redis.ts
│   │   └── providers.ts
│   └── types/                  # TypeScript types
│       ├── index.ts
│       ├── express.ts
│       └── api.ts
├── prisma/
│   ├── schema.prisma          # Database schema
│   └── seed.ts                # Database seeding
├── tests/
│   ├── auth.test.ts
│   ├── chat.test.ts
│   └── api.test.ts
└── package.json
```

## Data Models (Prisma Schema)

### Key Entities
1. **User** - User account information
2. **Conversation** - Chat sessions
3. **Message** - Individual chat messages
4. **Subscription** - User subscription details
5. **DemoPayment** - Demo payment transactions
6. **Usage** - API usage tracking
7. **GeneratedImage** - Image generation history
8. **GeneratedVideo** - Video generation history
9. **UploadedFile** - User uploaded files
10. **Settings** - Application configuration

## API Endpoints

### Authentication
- `POST /api/auth/signup` - Register new user
- `POST /api/auth/login` - Login user
- `POST /api/auth/refresh` - Refresh JWT token
- `POST /api/auth/logout` - Logout user
- `POST /api/auth/forgot-password` - Request password reset
- `POST /api/auth/reset-password` - Reset password
- `POST /api/auth/verify-email` - Verify email

### Chat
- `POST /api/chat/messages` - Send message
- `POST /api/chat/conversations` - Create conversation
- `GET /api/chat/conversations` - List conversations
- `GET /api/chat/conversations/:id` - Get conversation
- `PUT /api/chat/conversations/:id` - Update conversation
- `DELETE /api/chat/conversations/:id` - Delete conversation
- `POST /api/chat/messages/:id/regenerate` - Regenerate message
- `DELETE /api/chat/messages/:id` - Delete message

### Search
- `POST /api/search` - Perform web search

### Images
- `POST /api/images/generate` - Generate image
- `GET /api/images` - List generated images
- `DELETE /api/images/:id` - Delete image

### Videos
- `POST /api/videos/generate` - Generate video
- `GET /api/videos` - List videos
- `DELETE /api/videos/:id` - Delete video

### Files
- `POST /api/files/upload` - Upload file
- `GET /api/files` - List uploaded files
- `DELETE /api/files/:id` - Delete file
- `POST /api/files/:id/analyze` - Analyze file

### Users
- `GET /api/users/profile` - Get user profile
- `PUT /api/users/profile` - Update profile
- `PUT /api/users/password` - Change password
- `PUT /api/users/preferences` - Update preferences

### Subscriptions
- `GET /api/subscriptions/plans` - List pricing plans
- `GET /api/subscriptions/current` - Get current subscription
- `POST /api/subscriptions/upgrade` - Upgrade subscription
- `POST /api/subscriptions/cancel` - Cancel subscription

### Payments (Demo)
- `POST /api/payments/process` - Process demo payment
- `GET /api/payments/history` - Payment history

### Admin
- `GET /api/admin/users` - List users
- `PUT /api/admin/users/:id` - Update user
- `DELETE /api/admin/users/:id` - Delete user
- `GET /api/admin/stats` - Get statistics
- `PUT /api/admin/settings` - Update settings
- `GET /api/admin/payments` - Payment transactions

## Security Architecture

### Authentication Flow
1. User provides email and password
2. Backend hashes password with bcrypt
3. JWT token issued upon login
4. Token stored in secure HTTP-only cookie
5. Token included in Authorization header for API requests
6. Middleware verifies token on protected routes
7. Session data stored in Redis for quick access

### API Key Management
- All API keys stored in backend environment variables
- Never exposed to frontend
- Keys rotated periodically
- Usage logged and monitored

### Input Validation
- Zod schemas for all API endpoints
- Request validation in middleware
- File upload validation (size, type, extension)
- SQL injection prevention via ORM

## Deployment Pipeline

```
Local Development
       │
       ▼
Git Push → GitHub
       │
       ├─→ Frontend: Vercel CI/CD
       │        │
       │        ├─ Build Next.js
       │        ├─ Run tests
       │        └─ Deploy to Vercel
       │
       └─→ Backend: Render/Railway CI/CD
                │
                ├─ Run tests
                ├─ Database migrations
                └─ Deploy to Render
```

## Performance Optimization

- **Lazy Loading**: Components loaded on demand
- **Image Optimization**: Next.js Image component
- **Caching**: Redis for sessions and frequently accessed data
- **Database Indexing**: Indexes on frequently queried columns
- **API Rate Limiting**: Prevent abuse and DDoS
- **Connection Pooling**: Efficient database connections
- **CDN**: Static assets served via CDN

## Monitoring & Logging

- **Logging**: Winston/Pino for structured logs
- **Error Tracking**: Sentry integration
- **Performance Monitoring**: Datadog/New Relic
- **Uptime Monitoring**: StatusPage.io
- **Database Monitoring**: pg_stat_statements

## Future Enhancements

- [ ] Real payment processor integration (Paystack, Stripe)
- [ ] Mobile app (React Native)
- [ ] Team collaboration features
- [ ] Advanced analytics
- [ ] Custom AI model fine-tuning
- [ ] API for third-party integrations
- [ ] Webhook support
- [ ] Multi-language support
