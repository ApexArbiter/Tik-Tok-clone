# StreamVibe - Architecture Documentation

## Architecture Overview

StreamVibe follows a modern Next.js 14 App Router architecture with a component-based, service-oriented design pattern. The application is built with React and uses server-side rendering (SSR) and static site generation (SSG) for optimal performance.

## Application Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    Next.js App Router                    │
│  (Pages, Layouts, Route Handlers, Server Components)   │
└─────────────────────────────────────────────────────────┘
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
┌───────▼──────┐  ┌───────▼──────┐  ┌───────▼──────┐
│  Components  │  │   Services    │  │    Stores    │
│   (Client)   │  │   (API Calls) │  │   (Zustand)  │
└───────┬──────┘  └───────┬──────┘  └───────┬──────┘
        │                 │                 │
        └─────────────────┼─────────────────┘
                          │
                ┌─────────▼─────────┐
                │   Backend API     │
                │  (External API)  │
                └──────────────────┘
```

## Directory Structure

### `/src/app` - Next.js App Router

The App Router directory contains all routes and pages:

- **Dynamic Routes**: `[slug]` folders for dynamic content pages
- **Route Groups**: Organized by feature (movies, series, actors, etc.)
- **Layouts**: Shared layouts for route groups
- **Metadata**: SEO and Open Graph configuration

#### Key Routes:
- `/` - Home page
- `/movies` - Movie listing and detail pages
- `/series` - TV series listing and detail pages
- `/explore` - Content exploration and browsing
- `/actors/[slug]` - Actor detail pages
- `/directors/[slug]` - Director detail pages
- `/register` - Authentication pages (Login/Signup)
- `/subscriptions` - Subscription plans and management
- `/support` - Support and FAQ pages

### `/src/components` - React Components

Organized by feature and functionality:

#### Layout Components (`/layout`)
- `MainLayout.jsx` - Main application layout wrapper
- `navbar/` - Navigation bar components
- `footer/` - Footer components
- `singlePage/` - Layout for single content pages

#### Feature Components
- `home/` - Home page specific components
- `carousel/` - Image/content carousel
- `search/` - Search functionality components
- `review/` - Review and rating components
- `subscription/` - Subscription-related components
- `singlePage/` - Single movie/series page components
- `singleSeries/` - Series-specific components (seasons, episodes)
- `modal/` - Modal dialogs and overlays
- `question/` - FAQ components

#### Common Components (`/common`)
- `InputField.jsx` - Reusable input component
- `StarRating.jsx` - Star rating display/input

### `/src/services` - API Services

Service layer for API communication. Each service handles a specific domain:

- `MovieService.js` - Movie-related API calls
- `SeriesService.js` - TV series API calls
- `ActorService.js` - Actor information API calls
- `DirectorService.js` - Director information API calls
- `ReviewService.js` - Review and rating API calls
- `LikeService.js` - Like/favorite API calls
- `SubscriptionService.js` - Subscription API calls
- `SupportService.js` - Support/contact API calls

### `/src/stores` - State Management

Zustand stores for global state:

- `useUserStore.js` - User authentication and profile state

### `/src/constants` - Constants

- `Fonts.jsx` - Font configuration
- `PlansVariant.js` - Subscription plan variants
- `questions.js` - FAQ data

## Data Flow

### 1. Page Rendering Flow

```
User Request
    │
    ▼
Next.js App Router
    │
    ├─→ Server Component (Initial Render)
    │       │
    │       ├─→ Fetch Data (Server-side)
    │       │
    │       └─→ Render HTML
    │
    └─→ Client Component (Hydration)
            │
            ├─→ Use Services (API Calls)
            │
            ├─→ Update Store (Zustand)
            │
            └─→ Re-render UI
```

### 2. API Request Flow

```
Component
    │
    ▼
Service Function
    │
    ├─→ Fetch API (with NEXT_PUBLIC_API_URL)
    │
    ├─→ Handle Response
    │
    ├─→ Error Handling
    │
    └─→ Return Data
            │
            ▼
        Component State / Store
```

### 3. State Management Flow

```
User Action
    │
    ▼
Component Event Handler
    │
    ├─→ Direct State Update (useState)
    │
    └─→ Global State Update (Zustand Store)
            │
            ├─→ Store Action
            │
            └─→ API Call (if needed)
                    │
                    └─→ Update Store
                            │
                            └─→ Component Re-render
```

## Component Patterns

### 1. Server Components (Default)

Used for initial page loads and SEO-critical content:

```jsx
// Server Component (default)
export default async function Page() {
  const data = await fetchData();
  return <Component data={data} />;
}
```

### 2. Client Components

Used for interactivity, hooks, and browser APIs:

```jsx
"use client"
import { useState } from 'react';

export default function InteractiveComponent() {
  const [state, setState] = useState();
  // ... interactive logic
}
```

### 3. Service Pattern

Centralized API calls:

```javascript
// Service function
export const fetchMovies = async (page) => {
  const response = await fetch(`${API_URL}/movies?page=${page}`);
  return response.json();
};
```

### 4. Store Pattern

Global state with Zustand:

```javascript
const useStore = create((set) => ({
  data: null,
  fetchData: async () => {
    const data = await fetchData();
    set({ data });
  }
}));
```

## Routing Strategy

### Static Routes
- Home page (`/`)
- Main category pages (`/movies`, `/series`)

### Dynamic Routes
- Content detail pages (`/movies/[slug]`, `/series/[slug]`)
- Actor pages (`/actors/[slug]`)
- Director pages (`/directors/[slug]`)
- Genre pages (`/explore/[genres]`)

### Route Groups
- Organized by feature for better code organization
- Shared layouts within route groups

## API Integration

### API Base URL
All API calls use `process.env.NEXT_PUBLIC_API_URL` as the base URL.

### API Communication Pattern
1. Services make fetch requests to backend
2. Error handling at service level
3. Data transformation if needed
4. Return clean data to components

### Authentication
- Cookie-based authentication
- Credentials included in requests (`credentials: 'include'`)
- User state managed in Zustand store

## Performance Optimizations

### 1. Image Optimization
- Next.js Image component for optimized images
- Sharp for server-side image processing

### 2. Code Splitting
- Automatic code splitting by Next.js
- Dynamic imports for heavy components

### 3. Caching Strategy
- Static generation for static pages
- ISR (Incremental Static Regeneration) where applicable
- Client-side caching for API responses

### 4. Font Optimization
- Next.js font optimization
- Custom font loading with `@/constants/Fonts`

## Styling Architecture

### Tailwind CSS
- Utility-first CSS approach
- Custom color palette (e.g., `c-red-45`, `c-grey-60`)
- Responsive design with breakpoints
- Custom configuration in `tailwind.config.js`

### CSS Organization
- Global styles in `app/globals.css`
- Component-scoped styles with Tailwind classes
- No separate CSS files (utility-first approach)

## Build and Deployment

### Build Process
1. Next.js compiles React components
2. Generates static pages where possible
3. Optimizes images and assets
4. Creates production bundle

### Deployment
- Configured for Liara platform
- Environment variables required
- Production build with `npm run build`

## Security Considerations

1. **Environment Variables**: Sensitive data in `.env` files
2. **API Security**: Credentials sent securely
3. **XSS Prevention**: React's built-in XSS protection
4. **CSRF Protection**: Cookie-based auth with proper headers

## Scalability Considerations

1. **Component Reusability**: Shared components for common UI
2. **Service Layer**: Centralized API calls for easy updates
3. **State Management**: Scalable Zustand stores
4. **Code Organization**: Feature-based folder structure
5. **Performance**: SSR/SSG for fast initial loads

