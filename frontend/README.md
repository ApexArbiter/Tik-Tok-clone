# StreamVibe Frontend

StreamVibe is a modern streaming platform frontend built with Next.js 14, providing users with a comprehensive interface to watch and discover movies and TV shows online.

## 🚀 Quick Start

### Prerequisites
- Node.js (v18 or higher)
- npm, yarn, pnpm, or bun

### Installation

```bash
npm install
```

### Environment Setup

Create a `.env.local` file:

```env
NEXT_PUBLIC_API_URL=http://localhost:3001/api
NEXT_PUBLIC_BASE_URL=http://localhost:3000
```

### Development

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to view the application.

## 📚 Documentation

Comprehensive documentation is available in the following files:

- **[PROJECT_OVERVIEW.md](./PROJECT_OVERVIEW.md)** - Project overview, technology stack, and key features
- **[ARCHITECTURE.md](./ARCHITECTURE.md)** - Application architecture, data flow, and design patterns
- **[COMPONENTS.md](./COMPONENTS.md)** - Complete component documentation and usage
- **[SERVICES.md](./SERVICES.md)** - API service layer documentation
- **[SETUP.md](./SETUP.md)** - Detailed setup and development guide
- **[FEATURES.md](./FEATURES.md)** - Feature documentation and usage examples

## 🛠️ Available Scripts

- `npm run dev` - Start development server with Turbo
- `npm run build` - Build production bundle
- `npm run start` - Start production server
- `npm run lint` - Run ESLint

## 🏗️ Tech Stack

- **Framework**: Next.js 14.1.4 (App Router)
- **UI Library**: React 18
- **Styling**: Tailwind CSS 3.3.0
- **State Management**: Zustand 4.5.4
- **Forms**: React Hook Form 7.52.0
- **Animations**: React Spring 9.7.4
- **HTTP Client**: Axios 1.7.2

## 📁 Project Structure

```
frontend/
├── src/
│   ├── app/              # Next.js App Router pages
│   ├── components/       # React components
│   ├── services/         # API service functions
│   ├── stores/           # Zustand state stores
│   ├── constants/        # Constants and configuration
│   └── assets/           # Static assets
├── public/               # Public static files
└── docs/                 # Documentation files
```

## 🎯 Key Features

- 🎬 Movie and TV series browsing
- 🔍 Advanced search functionality
- ⭐ Reviews and ratings system
- 👤 User authentication
- 💳 Subscription management
- 📱 Responsive design
- 🚀 Optimized performance

## 📖 Learn More

- [Next.js Documentation](https://nextjs.org/docs)
- [React Documentation](https://react.dev)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)

## 🚢 Deployment

The application can be deployed to:
- **Vercel** (recommended for Next.js)
- **Liara** (configured)
- Any platform supporting Node.js

See [SETUP.md](./SETUP.md) for detailed deployment instructions.
