# StreamVibe - Setup & Development Guide

## Prerequisites

Before setting up the StreamVibe frontend, ensure you have the following installed:

- **Node.js** (v18 or higher recommended)
- **npm** (v9 or higher) or **yarn** or **pnpm** or **bun**
- **Git** (for version control)

## Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd frontend
```

### 2. Install Dependencies

Using npm:
```bash
npm install
```

Using yarn:
```bash
yarn install
```

Using pnpm:
```bash
pnpm install
```

Using bun:
```bash
bun install
```

## Environment Configuration

### 1. Create Environment File

Create a `.env.local` file in the root directory:

```bash
# .env.local
NEXT_PUBLIC_API_URL=http://localhost:3001/api
NEXT_PUBLIC_BASE_URL=http://localhost:3000
```

### 2. Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `NEXT_PUBLIC_API_URL` | Backend API base URL | `http://localhost:3001/api` |
| `NEXT_PUBLIC_BASE_URL` | Frontend base URL (for metadata) | `http://localhost:3000` |

**Note**: The `NEXT_PUBLIC_` prefix makes these variables available in the browser.

### 3. Production Environment

For production, create `.env.production`:

```bash
# .env.production
NEXT_PUBLIC_API_URL=https://api.streamvibe.com/api
NEXT_PUBLIC_BASE_URL=https://streamvibe.com
```

## Development

### Start Development Server

```bash
npm run dev
```

The application will start at [http://localhost:3000](http://localhost:3000)

The dev server uses Turbo mode for faster development experience.

### Development Scripts

| Script | Description |
|--------|-------------|
| `npm run dev` | Start development server with Turbo |
| `npm run build` | Build production bundle |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint for code linting |

## Project Structure

```
frontend/
├── .next/                 # Next.js build output (generated)
├── node_modules/          # Dependencies (generated)
├── public/                # Static files
│   ├── images/           # Image assets
│   └── github/           # GitHub assets
├── src/
│   ├── app/              # Next.js App Router pages
│   ├── components/       # React components
│   ├── services/         # API service functions
│   ├── stores/           # Zustand state stores
│   ├── constants/        # Constants and config
│   └── assets/           # Static assets
├── .env.local            # Local environment variables
├── .gitignore            # Git ignore rules
├── jsconfig.json         # JavaScript configuration
├── next.config.js        # Next.js configuration
├── package.json          # Dependencies and scripts
├── postcss.config.js     # PostCSS configuration
└── tailwind.config.js    # Tailwind CSS configuration
```

## Configuration Files

### next.config.js / next.config.mjs

Next.js configuration file. Configure:
- Image domains
- Redirects
- Headers
- Environment variables

### tailwind.config.js

Tailwind CSS configuration. Customize:
- Color palette
- Font families
- Breakpoints
- Plugins

### jsconfig.json

JavaScript/TypeScript path aliases:
```json
{
  "compilerOptions": {
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

This allows imports like:
```javascript
import Component from '@/components/Component';
```

## Development Workflow

### 1. Creating a New Page

Create a new file in `src/app/`:

```javascript
// src/app/new-page/page.jsx
export default function NewPage() {
  return <div>New Page</div>;
}
```

### 2. Creating a New Component

Create a component in `src/components/`:

```javascript
// src/components/NewComponent.jsx
export default function NewComponent() {
  return <div>New Component</div>;
}
```

### 3. Creating a New Service

Create a service file in `src/services/`:

```javascript
// src/services/NewService.js
export const fetchData = async () => {
  const response = await fetch(`${process.env.NEXT_PUBLIC_API_URL}/endpoint`);
  return response.json();
};
```

### 4. Using State Management

```javascript
// src/stores/useNewStore.js
import { create } from 'zustand';

const useNewStore = create((set) => ({
  data: null,
  setData: (data) => set({ data }),
}));

export default useNewStore;
```

## Code Style & Linting

### ESLint

The project uses ESLint with Next.js configuration:

```bash
npm run lint
```

### Code Formatting

Consider adding Prettier for consistent code formatting:

```bash
npm install --save-dev prettier
```

Create `.prettierrc`:
```json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2
}
```

## Building for Production

### 1. Build the Application

```bash
npm run build
```

This creates an optimized production build in `.next/` directory.

### 2. Start Production Server

```bash
npm run start
```

The production server runs on port 3000 by default.

### 3. Test Production Build Locally

```bash
npm run build
npm run start
```

## Deployment

### Deploy to Liara

The project is configured for Liara deployment:

1. Install Liara CLI:
```bash
npm install -g @liara/cli
```

2. Login to Liara:
```bash
liara login
```

3. Deploy:
```bash
liara deploy
```

### Deploy to Vercel

1. Install Vercel CLI:
```bash
npm install -g vercel
```

2. Deploy:
```bash
vercel
```

### Deploy to Other Platforms

The application can be deployed to any platform that supports Node.js:
- AWS
- Google Cloud Platform
- Azure
- DigitalOcean
- Heroku

## Troubleshooting

### Common Issues

#### 1. Port Already in Use

If port 3000 is already in use:

```bash
# Kill process on port 3000 (Windows)
netstat -ano | findstr :3000
taskkill /PID <PID> /F

# Or use a different port
npm run dev -- -p 3001
```

#### 2. Module Not Found

Clear cache and reinstall:

```bash
rm -rf node_modules .next
npm install
```

#### 3. Environment Variables Not Working

- Ensure variables start with `NEXT_PUBLIC_`
- Restart the dev server after adding variables
- Check `.env.local` is in the root directory

#### 4. Build Errors

Check for:
- Missing dependencies
- Type errors
- Import errors
- Environment variables

#### 5. API Connection Issues

- Verify `NEXT_PUBLIC_API_URL` is correct
- Check backend server is running
- Verify CORS settings on backend
- Check network connectivity

## Development Tips

### 1. Hot Reload

Next.js provides hot module replacement (HMR). Changes to files automatically refresh the browser.

### 2. Fast Refresh

React Fast Refresh preserves component state during development.

### 3. Debugging

Use browser DevTools:
- React DevTools extension
- Network tab for API calls
- Console for errors

### 4. Performance Monitoring

Use Next.js built-in analytics or add:
- Web Vitals
- Performance monitoring tools

### 5. Code Splitting

Next.js automatically code splits. Use dynamic imports for heavy components:

```javascript
import dynamic from 'next/dynamic';

const HeavyComponent = dynamic(() => import('@/components/HeavyComponent'));
```

## Testing (Future)

Consider adding:
- **Jest** - Unit testing
- **React Testing Library** - Component testing
- **Cypress** - E2E testing
- **Playwright** - E2E testing

## Additional Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [React Documentation](https://react.dev)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [Zustand Documentation](https://github.com/pmndrs/zustand)
- [React Hook Form Documentation](https://react-hook-form.com)

## Getting Help

- Check existing documentation
- Review code comments
- Check GitHub issues
- Contact the development team

