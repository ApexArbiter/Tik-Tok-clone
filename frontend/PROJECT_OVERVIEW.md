# StreamVibe - Project Overview

## Introduction

StreamVibe is a modern streaming platform frontend application built with Next.js 14. It provides users with a comprehensive interface to watch and discover movies and TV shows online. The platform offers a wide range of features including content browsing, user authentication, reviews, subscriptions, and more.

## Project Description

StreamVibe is designed to deliver the best streaming experience for watching favorite movies and shows on demand, anytime, anywhere. The platform features:

- **Vast Content Library**: Movies, TV series, documentaries, and exclusive original content
- **Multi-device Support**: Compatible with computers, smartphones, tablets, and smart TVs
- **User Accounts**: Registration, login, and personalized experiences
- **Reviews & Ratings**: User-generated reviews and ratings for content
- **Subscription Plans**: Multiple subscription tiers with different pricing options
- **Search Functionality**: Advanced search for movies, series, actors, and directors
- **Content Discovery**: Browse by genres, trending content, new releases, and popular titles

## Technology Stack

### Core Framework
- **Next.js 14.1.4** - React framework with App Router
- **React 18** - UI library
- **React DOM 18** - React rendering

### State Management
- **Zustand 4.5.4** - Lightweight state management

### Form Handling
- **React Hook Form 7.52.0** - Form validation and management

### UI & Styling
- **Tailwind CSS 3.3.0** - Utility-first CSS framework
- **PostCSS** - CSS processing
- **Autoprefixer** - CSS vendor prefixing

### UI Components & Animations
- **React Spring 9.7.4** - Animation library
- **React Use Gesture 9.1.3** - Gesture handling
- **React Rating 2.0.5** - Star rating component
- **React Toastify 10.0.5** - Toast notifications
- **SweetAlert2 11.12.0** - Beautiful alert dialogs

### HTTP Client
- **Axios 1.7.2** - HTTP client for API requests

### Development Tools
- **ESLint** - Code linting
- **Next.js ESLint Config** - Next.js specific linting rules
- **Sharp 0.33.4** - Image optimization

### Deployment
- **Liara CLI 7.0.7** - Deployment tool

## Project Structure

```
frontend/
├── src/
│   ├── app/                    # Next.js App Router pages
│   │   ├── actors/            # Actor pages
│   │   ├── directors/         # Director pages
│   │   ├── explore/           # Explore/browse pages
│   │   ├── movies/            # Movie pages
│   │   ├── register/          # Authentication pages
│   │   ├── series/            # TV series pages
│   │   ├── subscriptions/     # Subscription pages
│   │   ├── support/           # Support pages
│   │   └── page.jsx           # Home page
│   ├── components/            # React components
│   │   ├── carousel/          # Carousel components
│   │   ├── common/            # Shared components
│   │   ├── home/              # Home page components
│   │   ├── layout/            # Layout components
│   │   ├── modal/             # Modal components
│   │   ├── question/          # FAQ components
│   │   ├── review/            # Review components
│   │   ├── search/            # Search components
│   │   ├── singlePage/        # Single content page components
│   │   ├── singleSeries/      # Series page components
│   │   └── subscription/      # Subscription components
│   ├── services/              # API service functions
│   ├── stores/                # Zustand state stores
│   ├── constants/             # Constants and configuration
│   └── assets/                # Static assets
├── public/                     # Public static files
│   ├── images/                # Image assets
│   └── github/                # GitHub-related assets
├── package.json               # Dependencies and scripts
├── next.config.js            # Next.js configuration
├── tailwind.config.js        # Tailwind CSS configuration
└── README.md                 # Basic project readme
```

## Key Features

### 1. Content Browsing
- Browse movies and TV series by categories
- Filter by genres
- View trending, popular, and new releases
- Explore content by actors and directors

### 2. User Authentication
- User registration
- Login functionality
- User profile management
- Session management

### 3. Content Details
- Detailed movie/series pages
- Cast and crew information
- Reviews and ratings
- Download options
- Like/favorite functionality

### 4. Search
- Global search functionality
- Search movies, series, actors, and directors
- Real-time search results

### 5. Subscriptions
- Multiple subscription plans
- Plan comparison
- Free trial options
- Subscription management

### 6. Support
- FAQ section
- Contact/support form
- Help documentation

## Environment Variables

The application requires the following environment variables:

- `NEXT_PUBLIC_API_URL` - Backend API base URL
- `NEXT_PUBLIC_BASE_URL` - Frontend base URL (for metadata and images)

## Development Scripts

- `npm run dev` - Start development server with Turbo
- `npm run build` - Build production bundle
- `npm run start` - Start production server
- `npm run lint` - Run ESLint

## Browser Support

The application is designed to work on modern browsers and supports:
- Desktop browsers (Chrome, Firefox, Safari, Edge)
- Mobile browsers (iOS Safari, Chrome Mobile)
- Responsive design for tablets and smartphones

## Performance Features

- Image optimization with Sharp
- Font optimization with Next.js font system
- Code splitting and lazy loading
- Server-side rendering (SSR)
- Static site generation (SSG) where applicable

## Accessibility

- Semantic HTML structure
- ARIA labels where needed
- Keyboard navigation support
- Screen reader compatibility

## SEO Features

- Meta tags and Open Graph support
- Structured data
- Sitemap generation
- Robots.txt configuration
- Canonical URLs

