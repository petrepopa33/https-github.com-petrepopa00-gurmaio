# Gurmaio - Budget-Aware Meal Planning Platform

A production-ready, cloud-native meal planning application that generates budget-aware, nutrition-accurate meal plans with explicit cost calculation at all levels.

**🚀 Try it now on GitHub Spark:** This application is built with [GitHub Spark](https://githubnext.com/projects/spark/) and can be opened directly in your browser.

## 📁 Repository Structure

```
gurmaio/
├── PRD.md                    # Product Requirements Document
├── ARCHITECTURE.md           # Technical Architecture & Design
├── IMPLEMENTATION.md         # Step-by-step Implementation Guide
├── README.md                 # This file
├── spark.meta.json           # GitHub Spark metadata configuration
├── runtime.config.json       # Spark runtime settings
├── .spark-initial-sha        # Initial commit reference
├── vite.config.ts            # Vite configuration with Spark plugin
├── package.json              # Dependencies including @github/spark
└── src/                      # Application source code
    ├── components/           # UI Components
    ├── types/                # TypeScript Type Definitions
    ├── lib/                  # Utilities & Mock Data
    ├── hooks/                # Custom React hooks
    └── styles/               # CSS and styling
```

## 🎯 Project Overview

Gurmaio is designed as a commercial-grade meal planning platform with these core principles:

### Architecture
- **Edge-First**: Cloudflare Workers (280+ global locations)
- **Stateless**: No server-side sessions, JWT authentication
- **Deterministic**: All calculations reproducible and auditable
- **Separation of Concerns**: AI generates structure, engines calculate values

### Key Features
1. **Budget-First Planning**: Every meal plan respects user budget with transparent cost breakdowns
2. **Precise Nutrition**: Deterministic calculations for calories, protein, carbs, and fats at all levels
3. **Smart Shopping**: Aggregated shopping lists accounting for real-world grocery constraints
4. **GDPR Compliant**: Hard delete on account deletion
5. **Mobile-First**: Flutter app for iOS and Android

## 📚 Documentation

### 1. [PRD.md](./PRD.md)
Complete product requirements including:
- User experience design
- Feature specifications
- Edge case handling
- Visual design system (colors, typography, animations)
- Component selection

### 2. [ARCHITECTURE.md](./ARCHITECTURE.md)
Technical architecture documentation including:
- Cloud architecture diagrams
- API contract specifications
- Data models and schemas
- Deterministic engine pseudocode (nutrition, cost, shopping list)
- AI integration strategy
- Security & performance considerations

### 3. [IMPLEMENTATION.md](./IMPLEMENTATION.md)
Step-by-step implementation guide covering:
- Database setup (Supabase)
- Cloudflare Workers configuration
- Engine implementation
- API route development
- Flutter client integration
- Testing & deployment

## 🚀 Quick Start

### Option 1: Open in GitHub Spark (Recommended)

This application is built with GitHub Spark and can be opened directly in your browser without any local setup.

**How to open in Spark:**
1. Visit the repository on GitHub
2. Look for the "Open in Spark" button (if available in your Spark preview)
3. Alternatively, Spark applications are typically accessible through the GitHub Spark platform

Once opened in Spark:
- Sign in with your GitHub account
- Complete the onboarding flow with your preferences
- Start generating personalized meal plans immediately
- All data is automatically saved to your account

### Option 2: Local Development

For local development and customization:

#### Prerequisites
- Node.js 18+
- npm

#### Installation

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

### Features Available in Spark
- ✅ User authentication (GitHub OAuth)
- ✅ User onboarding flow
- ✅ Budget and dietary preference configuration
- ✅ Meal plan generation (with mock data)
- ✅ Multi-day meal plan visualization
- ✅ Nutrition and cost breakdowns at all levels
- ✅ Shopping list aggregation
- ✅ Meal plan persistence and history
- ✅ Meal ratings and substitutions
- ✅ Calendar scheduling and progress tracking
- ✅ Responsive design (mobile & desktop)

## 💡 About GitHub Spark

This application is built with [GitHub Spark](https://githubnext.com/projects/spark/), which provides:

- **Instant Deployment**: No build or deployment steps needed
- **Built-in Authentication**: GitHub OAuth integration
- **Data Persistence**: Key-value store for user data
- **No Server Required**: Runs entirely in the browser
- **Real-time Updates**: Instant feedback and state management

### Spark Integration

The application uses the following Spark features:

- **Spark KV Storage**: A key-value store that persists data to your GitHub account
  - Accessed via `useKV` React hook for state management
  - Also accessible via `window.spark.kv` API for direct operations
  - Both interfaces access the same underlying storage system
  - Data includes: meal plans, user profiles, shopping lists, ratings, and progress tracking
- **Spark Authentication**: GitHub OAuth authentication via `window.spark.user()`
  - Automatic login with your GitHub account
  - User profile information and avatar
  - Secure session management

All configuration is in:
- `spark.meta.json` - Spark metadata and template configuration
- `runtime.config.json` - Runtime application ID and settings
- `vite.config.ts` - Spark Vite plugin integration

## 🏗️ Production Implementation

### Technology Stack

#### Backend
- **Cloudflare Workers** - Serverless compute (Node.js runtime)
- **Supabase** - PostgreSQL database + authentication
- **OpenAI/Anthropic** - AI meal composition generation

#### Frontend
- **Flutter** - Cross-platform mobile app (iOS + Android)
- **Supabase Flutter SDK** - Authentication & API client

#### Infrastructure
- **Cloudflare** - Edge network, CDN, DDoS protection
- **Supabase** - Managed Postgres with connection pooling
- **GitHub Actions** - CI/CD pipeline

### Architecture Components

```
┌─────────────┐
│ Flutter App │
│ (iOS/Android)│
└──────┬──────┘
       │ JWT Auth
       ▼
┌─────────────────┐
│ Cloudflare      │
│ Workers API     │◄────┐
└────────┬────────┘     │
         │              │
    ┌────▼────┐   ┌─────┴─────┐
    │Supabase │   │  AI API   │
    │Postgres │   │(OpenAI)   │
    └─────────┘   └───────────┘
```

### Deployment Pipeline

1. **Database**: Supabase migrations applied
2. **API**: `wrangler deploy` to Cloudflare Workers
3. **Mobile**: Flutter build → App Store + Play Store

## 🔑 Key Design Decisions

### Why Cloudflare Workers?
- Sub-200ms global latency
- Auto-scaling to millions of requests
- No cold starts
- Cost-effective ($5/month for 10M requests)

### Why Separate AI from Calculations?
- **Reproducibility**: Same inputs = same outputs
- **Auditability**: Every cost/nutrition value traceable
- **Trust**: Users can verify calculations
- **Testability**: Deterministic engines easy to unit test

### Why Flutter?
- Single codebase for iOS + Android
- Native performance
- Rich UI component library
- Strong typing with Dart

## 📊 Data Flow

### Meal Plan Generation

```
User → Profile Config → API
                        ↓
                  AI Generates Structure
                    (JSON meals)
                        ↓
                Nutrition Engine
            (Calculate per ingredient)
                        ↓
                   Cost Engine
            (Calculate per ingredient)
                        ↓
              Aggregate to Meal Level
                        ↓
              Aggregate to Day Level
                        ↓
              Aggregate to Plan Level
                        ↓
              Validate Against Budget
                        ↓
            ┌───────────┴───────────┐
            │                       │
        Over Budget?           Within Budget
            │                       │
    Retry with                 Save to DB
    Tighter Constraints            │
            │                       │
            └───────────┬───────────┘
                        ↓
                Return to Client
```

## 🧪 Testing Strategy

### Unit Tests
- Nutrition engine calculations
- Cost engine calculations
- Budget validation logic
- Shopping list aggregation

### Integration Tests
- API endpoint responses
- Database queries
- RLS policies

### End-to-End Tests
- Complete user flows
- Multi-day generation
- Budget enforcement scenarios

## 🔐 Security

- JWT authentication via Supabase
- Row-Level Security (RLS) for all user data
- Service role key never exposed to client
- Input validation with Zod schemas
- Rate limiting via Cloudflare
- CORS whitelist

## 📈 Performance Targets

- **API Response Time**: < 200ms (p95)
- **AI Generation Time**: < 10s for 7-day plan
- **Shopping List**: < 100ms
- **Database Queries**: < 50ms per query
- **Global Edge Latency**: < 50ms

## 🌍 Compliance

- **GDPR**: Hard delete on account deletion
- **App Store**: Follows Apple Human Interface Guidelines
- **Play Store**: Follows Material Design principles
- **Accessibility**: WCAG AA contrast ratios

## 📱 Mobile App Features

- [ ] Biometric authentication
- [ ] Offline mode (cached meal plans)
- [ ] Push notifications (meal reminders)
- [ ] Dark mode
- [ ] Multi-language support
- [ ] In-app purchases (premium features)
- [ ] Social sharing
- [ ] Barcode scanner (shopping list)

## 🚧 Roadmap

### Phase 1: MVP (Current)
- ✅ Core meal plan generation
- ✅ Budget enforcement
- ✅ Shopping list generation
- ✅ User authentication

### Phase 2: Enhanced Features
- [ ] Meal plan history
- [ ] Ingredient substitutions
- [ ] Recipe details & instructions
- [ ] Favorites & custom meals

### Phase 3: Social & Integration
- [ ] Share meal plans with friends
- [ ] Grocery delivery API integration
- [ ] Fitness app integration
- [ ] Nutritionist review system

### Phase 4: Intelligence
- [ ] ML-based preference learning
- [ ] Seasonal ingredient suggestions
- [ ] Local grocery price updates
- [ ] Personalized recommendations

## 💰 Business Model

### Freemium
- **Free Tier**: 1 meal plan per week
- **Premium**: $9.99/month
  - Unlimited meal plans
  - Advanced filters (low-sodium, keto, etc.)
  - Recipe instructions
  - Grocery delivery integration
  - Priority support

### B2B
- Corporate wellness programs
- Fitness center partnerships
- Healthcare provider integrations

## 🤝 Contributing

This is a design and architecture reference. For production implementation:

1. Review all documentation files
2. Set up development environment per IMPLEMENTATION.md
3. Follow coding standards in architecture docs
4. Write tests for all new features
5. Deploy to staging before production

## 📄 License

MIT License - See LICENSE file for details

## 📞 Contact & Support

For questions about this architecture:
- Review the documentation files first
- Check implementation guide for setup issues
- Consult architecture doc for design decisions

---

**Built with precision. Designed for scale. Ready for production.**
