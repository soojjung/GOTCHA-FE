# GOTCHA! – Gacha Shop Map Service

<p align="center">
  <img src="appstore-assets/screenshots/iPad13Air/앱미리보기(아이패드)_1인트로.png" alt="GOTCHA! App Intro Screen 1" width="49%" />
  <img src="appstore-assets/screenshots/iPad13Air/앱미리보기(아이패드)_2인트로.png" alt="GOTCHA! App Intro Screen 2" width="49%" />
</p>

A mobile web service for discovering Gacha Shops on a map, browsing store listings, and viewing detailed shop information.

[![Download on the App Store](https://developer.apple.com/assets/elements/badges/download-on-the-app-store.svg)](https://apps.apple.com/kr/app/id6759491099)

---

## Key Features

- 🗺️ Kakao Map-based gacha shop discovery
- 🏪 Store details & reviews
- ⭐ Favorites
- 📝 New shop submissions
- 🚨 Review/shop/user reporting & blocking
- 🔔 Web Push notifications
- 📱 PWA support
- 📲 Available on iOS App Store

### Upcoming

- 🤖 AI-powered character name recognition

---

## Tech Stack

### Frontend

- Next.js 16 (App Router)
- React 19
- TypeScript
- Tailwind CSS
- Zustand
- TanStack Query
- Kakao Map SDK
- Lucide React (icons)
- PWA support
- Capacitor (iOS native app)
- Vercel

### Backend

- Spring Boot 3.x
- Java 21
- Spring Data JPA
- PostgreSQL
- Swagger
- AWS EC2 / S3

🔗 Backend repository: [GOTCHA-BE](https://github.com/fcde-project9/GOTCHA-BE)

---

## Architecture Patterns

| Area             | Pattern                                        |
| ---------------- | ---------------------------------------------- |
| State Management | Zustand (global) + TanStack Query (server)     |
| API Layer        | API Wrapper (`request.ts`) + Query Key Factory |
| Error Handling   | QueryErrorBoundary                             |
| Authentication   | Zustand Persist                                |

📖 Details: [`.ai/architecture.md`](.ai/architecture.md) | [`.ai/coding_standards.md`](.ai/coding_standards.md)

---

## CI/CD

Automated deployment pipeline using GitHub Actions + Vercel

| Branch | Environment | URL                                            |
| ------ | ----------- | ---------------------------------------------- |
| `dev`  | Preview     | [dev.gotcha.it.com](https://dev.gotcha.it.com) |
| `main` | Production  | [gotcha.it.com](https://gotcha.it.com)         |

**Deployment Process**: Code push → Lint check → Build → Vercel deploy

---

## Development Setup

### Prerequisites

- Node.js 24 or higher
- npm 9 or higher

### Installation & Running

1. Set Node version (if using nvm)

   ```bash
   nvm use
   ```

2. Install dependencies

   ```bash
   npm install
   ```

3. Configure environment variables

   ```bash
   cp .env.example .env.local
   # Open .env.local and fill in the actual values
   ```

4. Start the development server

   ```bash
   npm run dev
   ```

   Open [http://localhost:3000](http://localhost:3000)

### Available Scripts

| Command                   | Description                                      |
| ------------------------- | ------------------------------------------------ |
| `npm run dev`             | Start dev server (localhost:3000)                |
| `npm run build`           | Production build                                 |
| `npm run start`           | Start production server                          |
| `npm run dev:ios`         | Run iOS simulator with dev server                |
| `npm run build:capacitor` | Production build for Capacitor target            |
| `npm run build:ios`       | Capacitor build + iOS sync + open Xcode          |
| `npm run lint`            | Run ESLint                                       |
| `npm run lint:fix`        | Auto-fix ESLint issues                           |
| `npm run format`          | Run Prettier formatting (all project files)      |

### Git Hooks (Husky)

Code quality checks run automatically on commit.

```text
pre-commit → lint-staged → ESLint + Prettier
```

| File Type           | Action                               |
| ------------------- | ------------------------------------ |
| `*.{js,jsx,ts,tsx}` | ESLint auto-fix + Prettier format    |
| `*.{json,css,md}`   | Prettier format                      |

> Commits will be blocked if there are lint errors. Run `npm run lint:fix` first.

---

## Project Structure

```
src/
├── app/           # Next.js App Router (pages)
├── components/    # Components (common, features, mypage, report, etc.)
├── api/           # API client, queries, mutations
├── stores/        # Zustand state management
├── hooks/         # Custom hooks
├── types/         # TypeScript types
├── utils/         # Utility functions
├── constants/     # Constants
├── styles/        # Styles
└── lib/           # External library utilities
```

---

## AI Documentation (.ai folder)

The `.ai/` folder contains standard documentation referenced by both AI tools (Claude, Cursor, etc.) and developers.

### Document List

| File                                | Description                                        |
| ----------------------------------- | -------------------------------------------------- |
| `daily-learnings/`                  | Daily learning notes (generated via `/wrap` command)|
| `initial_setting.md`                | Project initial setup guide                        |
| `coding_standards.md`               | Coding conventions & naming rules                  |
| `nextjs16_best_practices.md`        | Next.js 16 + React 19 best practices               |
| `nextjs16_migration_guide.md`       | Next.js 16 migration guide                         |
| `seo_standards.md`                  | SEO optimization guide                             |
| `modal_and_permission_standards.md` | Modal & permission request UI standards            |
| `button_component.md`              | Button component usage guide                       |
| `user_role_permissions.md`          | User role permission definitions                   |
| `google_analytics.md`              | Google Analytics setup guide                       |
| `capacitor_ios_setup.md`           | Capacitor iOS app wrapping documentation           |

### How to Use

1. **AI Tool Context**: Reference `.ai/` docs when writing code with Claude Code, Cursor, etc. to generate code that follows project conventions

2. **Onboarding**: Helps new developers quickly understand project standards

3. **Consistency**: Standardizes coding styles, component patterns, SEO settings, etc.

4. **Learning Records**: Share knowledge within the team by documenting new concepts in `daily-learnings/`

### Documentation Update Policy

- If code and documentation are out of sync, update `.ai/` docs first, then reflect in code
- When introducing new patterns or conventions, updating related documentation is required
