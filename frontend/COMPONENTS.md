# StreamVibe - Components Documentation

## Component Overview

The StreamVibe application uses a component-based architecture with React components organized by feature and functionality. This document provides an overview of all components and their purposes.

## Component Categories

### Layout Components

#### MainLayout (`/layout/MainLayout.jsx`)
Main application wrapper that provides the overall page structure.

#### Navbar Components (`/layout/navbar/`)
- **Navbar.jsx** - Main navigation bar
- **NavbarNav.jsx** - Navigation menu items
- **Search.jsx** - Search functionality in navbar
- **NotificationButton.jsx** - Notification button component

#### Footer Components (`/layout/footer/`)
- **Footer.jsx** - Main footer component
- **FooterNav.jsx** - Footer navigation links
- **FooterSocial.jsx** - Social media links
- **Copyright.jsx** - Copyright information

#### Single Page Layout (`/layout/singlePage/`)
- **SinglePageLayout.jsx** - Layout for single content pages
- **SinglePageSkeleton.jsx** - Loading skeleton for single pages
- **Sidebar.jsx** - Sidebar component for single pages

### Home Page Components (`/home/`)

#### HomeBanner.jsx
Hero banner component displayed on the home page.

#### HomeTitle.jsx
Main title and description section with call-to-action button.

#### HomeMovieCategory.jsx
Displays movie categories on the home page.

#### HomeExperience.jsx
Shows the streaming experience across various devices.

#### ExperienceItem.jsx
Individual experience item component.

#### ExperienceTitle.jsx
Title and description for the experience section.

#### ExperienceVariant.jsx
Variants of experience display.

#### MovieCategoryTitle.jsx
Title component for movie categories.

### Carousel Components (`/carousel/`)

#### Carousel.jsx
Main carousel component for displaying images/content.

#### CarouselInfo.jsx
Information overlay on carousel items.

#### CarouselCallToAction.jsx
Call-to-action buttons in carousel.

#### CarouselPagination.jsx
Pagination dots/indicators for carousel.

### Search Components (`/search/`)

#### SearchBox.jsx
Main search input box component.

#### SearchForm.jsx
Search form wrapper component.

#### SearchContainer.jsx
Container for search results.

#### SearchOverlay.jsx
Overlay that appears when search is active.

#### SearchMovieItem.jsx
Individual movie item in search results.

#### SearchMovieItemSkeleton.jsx
Loading skeleton for movie search items.

#### SearchActorItem.jsx
Individual actor item in search results.

#### ActorItemInfo.jsx
Information display for actor items.

#### ActoritemProfile.jsx
Actor profile image/thumbnail.

#### MovieItemInfo.jsx
Information display for movie items.

#### MovieItemThumbnail.jsx
Movie thumbnail image.

### Single Page Components (`/singlePage/`)

#### TopHeader.jsx
Header section of single content page.

#### Description.jsx
Content description section.

#### Rating.jsx
Rating display component.

#### Genres.jsx
Genre tags display.

#### Languages.jsx
Available languages display.

#### ReleasedMovie.jsx
Release date information.

#### Director.jsx
Director information display.

#### Musician.jsx
Music/composer information.

#### CastSection.jsx
Cast members section.

#### ActorItem.jsx
Individual actor card in cast section.

#### DownloadSection.jsx
Download options section.

#### DownloadItem.jsx
Individual download option item.

#### HeaderCallToAction.jsx
Call-to-action buttons in header.

#### LikeButton.jsx
Like/favorite button component.

### Series Components (`/singleSeries/`)

#### SeasonsSection.jsx
Section displaying all seasons.

#### SeasonItem.jsx
Individual season card.

#### SeasonItemSkeleton.jsx
Loading skeleton for season items.

#### EpisodeItem.jsx
Individual episode card.

#### EpisodeItemInfo.jsx
Episode information display.

#### EpisodeItemThumbnail.jsx
Episode thumbnail image.

### Review Components (`/review/`)

#### ReviewSection.jsx
Main reviews section container.

#### ReviewSectionTitle.jsx
Title for reviews section.

#### ReviewItem.jsx
Individual review card.

#### ReviewItemSkeleton.jsx
Loading skeleton for review items.

#### AddReviewForm.jsx
Form for adding new reviews.

### Subscription Components (`/subscription/`)

#### SubscriptionPlan.jsx
Main subscription plans display.

#### SubscriptionPlanTitle.jsx
Title for subscription section.

#### SubscriptionPlanContent.jsx
Content wrapper for plans.

#### SubscriptionPlanItem.jsx
Individual subscription plan card.

#### SubscriptionPlanSkeleton.jsx
Loading skeleton for plans.

#### SubscriptionPlanToggle.jsx
Toggle for plan duration (monthly/yearly).

#### SubscriptionBox.jsx
Subscription box/CTA component.

#### SubscriptionModalContent.jsx
Modal content for subscription.

#### FreeTrialModalContent.jsx
Modal content for free trial.

### Question/FAQ Components (`/question/`)

#### AskedQuestions.jsx
Main FAQ section component.

#### QuestionTitle.jsx
Title for FAQ section.

#### QuestionItem.jsx
Individual FAQ item (expandable).

#### QuestionForm.jsx
Form for submitting questions.

### Modal Components (`/modal/`)

#### DialogModal.jsx
Main dialog modal component.

#### ModalContent.jsx
Content wrapper for modals.

#### Overlay.jsx
Modal overlay/backdrop.

#### DraggableModal.jsx
Draggable modal component.

### Common Components (`/common/`)

#### InputField.jsx
Reusable input field component with validation support.

**Props:**
- `label` - Input label
- `name` - Input name
- `type` - Input type
- `placeholder` - Placeholder text
- `register` - React Hook Form register function
- `error` - Error message

#### StarRating.jsx
Star rating display/input component.

**Props:**
- `rating` - Current rating value
- `onChange` - Rating change handler (optional)
- `readonly` - Whether rating is read-only

### Form Components

#### FormField.jsx
Generic form field wrapper component.

#### TextAreaField.jsx
Textarea input component.

#### CheckboxField.jsx
Checkbox input component.

### Card Components

#### MovieCard.jsx
Card component for displaying movie information.

**Features:**
- Movie thumbnail
- Title
- Rating
- Genre tags
- Hover effects

#### MovieCardSkeleton.jsx
Loading skeleton for movie cards.

#### MultipleCard.jsx
Card component for displaying multiple items (movies/series).

#### MultipleCardSkeleton.jsx
Loading skeleton for multiple cards.

### Utility Components

#### PaginationToggle.jsx
Toggle component for pagination controls.

#### SlidePagination.jsx
Pagination component for carousels/sliders.

## Component Patterns

### 1. Container/Presentational Pattern

Many components follow a container/presentational pattern:
- Container components handle data fetching and state
- Presentational components handle UI rendering

### 2. Skeleton Loading Pattern

Components have corresponding skeleton versions for loading states:
- `MovieCard.jsx` → `MovieCardSkeleton.jsx`
- `ReviewItem.jsx` → `ReviewItemSkeleton.jsx`
- `SearchMovieItem.jsx` → `SearchMovieItemSkeleton.jsx`

### 3. Composition Pattern

Complex components are built from smaller, reusable components:
- `HomeExperience.jsx` uses `ExperienceItem.jsx`, `ExperienceTitle.jsx`
- `ReviewSection.jsx` uses `ReviewItem.jsx`, `ReviewSectionTitle.jsx`

### 4. Client Component Pattern

Components that need interactivity use the `"use client"` directive:
- Components with hooks (useState, useEffect)
- Components with event handlers
- Components using browser APIs

## Component Props Patterns

### Common Props

Many components share common prop patterns:

```jsx
// Data props
data={...}
items={...}
movies={...}

// Styling props
className={...}
variant={...}

// Event handlers
onClick={...}
onChange={...}
onSubmit={...}

// Loading states
loading={...}
skeleton={...}

// Configuration
limit={...}
page={...}
```

## Component Reusability

### Highly Reusable Components
- `InputField.jsx` - Used across all forms
- `MovieCard.jsx` - Used in multiple listing pages
- `StarRating.jsx` - Used in reviews and ratings
- `Modal` components - Used for various dialogs

### Feature-Specific Components
- Home page components - Only used on home page
- Single page components - Only used on detail pages
- Series components - Only used for TV series

## Component Dependencies

### External Libraries
- **React Hook Form** - Form components
- **React Rating** - Star rating component
- **React Spring** - Animation components
- **React Toastify** - Toast notifications
- **SweetAlert2** - Alert dialogs

### Internal Dependencies
- Services - Components use service functions for API calls
- Stores - Components use Zustand stores for global state
- Constants - Components use constants for configuration

## Best Practices

1. **Component Naming**: PascalCase for component files
2. **Props Validation**: Use PropTypes or TypeScript (if added)
3. **Error Handling**: Components handle errors gracefully
4. **Loading States**: Skeleton components for better UX
5. **Accessibility**: Semantic HTML and ARIA labels
6. **Responsive Design**: Mobile-first approach with Tailwind
7. **Performance**: Memoization where needed, lazy loading for heavy components

## Component Testing Considerations

When adding tests, consider:
- Unit tests for presentational components
- Integration tests for container components
- Snapshot tests for UI consistency
- Accessibility tests for WCAG compliance

