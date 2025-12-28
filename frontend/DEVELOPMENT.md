# StreamVibe - Development Guide

## Development Workflow

### 1. Setting Up Development Environment

Follow the steps in [SETUP.md](./SETUP.md) to set up your development environment.

### 2. Code Organization

#### File Naming Conventions
- **Components**: PascalCase (e.g., `MovieCard.jsx`)
- **Services**: PascalCase with "Service" suffix (e.g., `MovieService.js`)
- **Stores**: camelCase with "use" prefix (e.g., `useUserStore.js`)
- **Constants**: PascalCase (e.g., `Fonts.jsx`)
- **Pages**: lowercase with hyphens in routes (e.g., `page.jsx`)

#### Component Structure
```jsx
// 1. Imports
import React from 'react';
import { useState } from 'react';

// 2. Component definition
const ComponentName = ({ prop1, prop2 }) => {
  // 3. Hooks
  const [state, setState] = useState();
  
  // 4. Event handlers
  const handleClick = () => {
    // Handler logic
  };
  
  // 5. Render
  return (
    <div>
      {/* JSX */}
    </div>
  );
};

// 6. Export
export default ComponentName;
```

### 3. Adding New Features

#### Step 1: Create Component
```bash
# Create component file
touch src/components/NewFeature/NewComponent.jsx
```

#### Step 2: Implement Component
```jsx
"use client" // If using hooks
import React from 'react';

const NewComponent = () => {
  return <div>New Component</div>;
};

export default NewComponent;
```

#### Step 3: Create Service (if needed)
```bash
# Create service file
touch src/services/NewService.js
```

```javascript
export const fetchNewData = async () => {
  const response = await fetch(`${process.env.NEXT_PUBLIC_API_URL}/new-endpoint`);
  return response.json();
};
```

#### Step 4: Add Route (if needed)
```bash
# Create page file
mkdir -p src/app/new-feature
touch src/app/new-feature/page.jsx
```

#### Step 5: Test Feature
- Test in development mode
- Check responsive design
- Test error scenarios
- Verify accessibility

### 4. Component Development Best Practices

#### Use Client Components When Needed
```jsx
"use client"
// Use for:
// - useState, useEffect, other hooks
// - Event handlers
// - Browser APIs
// - Third-party libraries requiring client-side
```

#### Keep Server Components Default
```jsx
// Default: Server Component
// Use for:
// - Initial data fetching
// - SEO-critical content
// - Static content
```

#### Error Handling
```jsx
const Component = () => {
  const [error, setError] = useState(null);
  
  const fetchData = async () => {
    try {
      const data = await fetchData();
      // Handle success
    } catch (err) {
      setError(err.message);
      // Show error to user
    }
  };
  
  if (error) return <ErrorDisplay error={error} />;
  // ...
};
```

#### Loading States
```jsx
const Component = () => {
  const [loading, setLoading] = useState(true);
  const [data, setData] = useState(null);
  
  useEffect(() => {
    const loadData = async () => {
      setLoading(true);
      const result = await fetchData();
      setData(result);
      setLoading(false);
    };
    loadData();
  }, []);
  
  if (loading) return <SkeletonComponent />;
  if (!data) return <EmptyState />;
  
  return <DataDisplay data={data} />;
};
```

### 5. State Management

#### Local State (useState)
```jsx
// Use for component-specific state
const [count, setCount] = useState(0);
```

#### Global State (Zustand)
```jsx
// Use for shared state across components
import useUserStore from '@/stores/useUserStore';

const Component = () => {
  const { user, fetchUser } = useUserStore();
  // ...
};
```

#### Form State (React Hook Form)
```jsx
import { useForm } from 'react-hook-form';

const FormComponent = () => {
  const { register, handleSubmit, formState: { errors } } = useForm();
  
  const onSubmit = (data) => {
    // Handle form submission
  };
  
  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register('field', { required: true })} />
      {errors.field && <span>Error message</span>}
    </form>
  );
};
```

### 6. API Integration

#### Service Functions
```javascript
// src/services/NewService.js
export const fetchData = async (params) => {
  try {
    const response = await fetch(
      `${process.env.NEXT_PUBLIC_API_URL}/endpoint?param=${params}`,
      {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
        },
        credentials: 'include', // For authenticated requests
      }
    );
    
    if (!response.ok) {
      throw new Error('Request failed');
    }
    
    return await response.json();
  } catch (error) {
    console.error('API Error:', error);
    throw error;
  }
};
```

#### Using Services in Components
```jsx
import { fetchData } from '@/services/NewService';

const Component = () => {
  const [data, setData] = useState(null);
  
  useEffect(() => {
    const loadData = async () => {
      try {
        const result = await fetchData();
        setData(result);
      } catch (error) {
        // Handle error
      }
    };
    loadData();
  }, []);
  
  // ...
};
```

### 7. Styling Guidelines

#### Tailwind CSS Classes
```jsx
// Use Tailwind utility classes
<div className="flex items-center justify-between p-4 bg-white rounded-lg shadow-md">
  <h2 className="text-2xl font-bold text-gray-800">Title</h2>
  <button className="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600">
    Button
  </button>
</div>
```

#### Responsive Design
```jsx
// Mobile-first approach
<div className="
  text-sm md:text-base lg:text-lg xl:text-xl
  p-2 md:p-4 lg:p-6
  grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3
">
  {/* Content */}
</div>
```

#### Custom Colors
```jsx
// Use custom color palette
<div className="bg-c-red-45 text-white">
  {/* Custom colors defined in tailwind.config.js */}
</div>
```

### 8. Testing Considerations

#### Component Testing
```javascript
// Example test structure (when adding testing)
import { render, screen } from '@testing-library/react';
import Component from './Component';

describe('Component', () => {
  it('renders correctly', () => {
    render(<Component />);
    expect(screen.getByText('Expected Text')).toBeInTheDocument();
  });
});
```

#### Service Testing
```javascript
// Mock API calls
global.fetch = jest.fn(() =>
  Promise.resolve({
    json: () => Promise.resolve({ data: 'test' }),
  })
);
```

### 9. Performance Optimization

#### Image Optimization
```jsx
import Image from 'next/image';

<Image
  src="/images/example.jpg"
  alt="Description"
  width={500}
  height={300}
  priority // For above-the-fold images
/>
```

#### Code Splitting
```jsx
import dynamic from 'next/dynamic';

// Lazy load heavy components
const HeavyComponent = dynamic(() => import('@/components/HeavyComponent'), {
  loading: () => <SkeletonComponent />,
});
```

#### Memoization
```jsx
import { useMemo, memo } from 'react';

// Memoize expensive calculations
const expensiveValue = useMemo(() => {
  return computeExpensiveValue(data);
}, [data]);

// Memoize components
const MemoizedComponent = memo(({ prop }) => {
  return <div>{prop}</div>;
});
```

### 10. Accessibility

#### Semantic HTML
```jsx
// Use semantic elements
<header>
  <nav>
    <ul>
      <li><a href="/">Home</a></li>
    </ul>
  </nav>
</header>

<main>
  <article>
    <h1>Title</h1>
    <p>Content</p>
  </article>
</main>
```

#### ARIA Labels
```jsx
<button
  aria-label="Close modal"
  aria-expanded={isOpen}
  onClick={handleClose}
>
  ×
</button>
```

#### Keyboard Navigation
```jsx
const handleKeyDown = (e) => {
  if (e.key === 'Enter' || e.key === ' ') {
    handleClick();
  }
};

<button
  onClick={handleClick}
  onKeyDown={handleKeyDown}
  tabIndex={0}
>
  Click me
</button>
```

### 11. Git Workflow

#### Branch Naming
- `feature/feature-name` - New features
- `fix/bug-description` - Bug fixes
- `refactor/component-name` - Refactoring
- `docs/documentation-update` - Documentation

#### Commit Messages
```
feat: Add movie search functionality
fix: Fix pagination issue on movies page
refactor: Refactor MovieCard component
docs: Update API documentation
style: Format code with Prettier
test: Add tests for MovieService
```

### 12. Code Review Checklist

Before submitting code for review:
- [ ] Code follows project conventions
- [ ] Components are properly structured
- [ ] Error handling is implemented
- [ ] Loading states are handled
- [ ] Responsive design is verified
- [ ] Accessibility is considered
- [ ] No console.logs in production code
- [ ] Environment variables are properly used
- [ ] API calls include error handling
- [ ] Code is properly commented

### 13. Debugging

#### Browser DevTools
- React DevTools for component inspection
- Network tab for API calls
- Console for errors and logs
- Performance tab for performance issues

#### Next.js Debugging
```bash
# Run with debug logging
NODE_OPTIONS='--inspect' npm run dev
```

#### Common Issues
1. **Hydration Errors**: Check for mismatches between server and client
2. **API Errors**: Verify API URL and CORS settings
3. **Styling Issues**: Check Tailwind classes and custom CSS
4. **State Issues**: Verify state management and updates

### 14. Documentation

When adding new features:
1. Update relevant documentation files
2. Add code comments for complex logic
3. Document API endpoints in API_DOCUMENTATION.md
4. Update component documentation in COMPONENTS.md
5. Add usage examples in FEATURES.md

### 15. Resources

- [Next.js Docs](https://nextjs.org/docs)
- [React Docs](https://react.dev)
- [Tailwind CSS Docs](https://tailwindcss.com/docs)
- [Zustand Docs](https://github.com/pmndrs/zustand)
- [React Hook Form Docs](https://react-hook-form.com)

## Getting Help

- Check existing documentation
- Review similar components in the codebase
- Check GitHub issues
- Ask the development team

