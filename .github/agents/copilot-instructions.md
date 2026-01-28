# GitHub Copilot Agent Instructions

## Project Overview
This is a **Code Wiki** application built with TanStack Router and React. The project aims to provide a wiki-style interface for documenting code and technical knowledge.

## Tech Stack
- **Framework**: React 19.2.0 with TanStack Router
- **Build Tool**: Vite
- **Testing**: Vitest with Testing Library
- **Styling**: CSS
- **TypeScript**: Type-safe codebase

## Development Guidelines

### Code Style
- Use TypeScript for all new files
- Follow React functional component patterns with hooks
- Use TanStack Router conventions for routing
- Keep components modular and reusable
- Write tests for new features using Vitest

### File Structure
- `/src/routes/` - Route components (file-based routing)
- `/src/components/` - Reusable React components
- `/src/data/` - Data management and utilities
- `/src/styles.css` - Global styles

### Testing
- Write unit tests for new components and utilities
- Use Testing Library for React component tests
- Run tests with `npm run test`
- Ensure tests pass before committing

### Routing
- Use file-based routing with TanStack Router
- Route files go in `src/routes/`
- Use `<Link>` component for navigation
- Implement layouts in `src/routes/__root.tsx`

### Best Practices
- Keep components small and focused
- Use TypeScript types for props and state
- Avoid inline styles, use CSS modules or global styles
- Test edge cases and error states
- Document complex logic with comments
- Follow existing code patterns in the repository

### Common Tasks

#### Adding a New Route
1. Create a new file in `src/routes/`
2. Use TanStack Router's route creation pattern
3. Implement the component with proper TypeScript types
4. Add navigation links where appropriate

#### Adding a New Component
1. Create component in `src/components/`
2. Define TypeScript interface for props
3. Implement the component with proper typing
4. Write tests in a co-located `.test.tsx` file
5. Export from component directory if needed

#### Data Fetching
- Use TanStack Router loaders for route-level data
- Consider React Query for complex data fetching needs
- Handle loading and error states properly

### Performance Considerations
- Keep bundle size small
- Use lazy loading for routes when appropriate
- Optimize re-renders with proper React patterns
- Profile performance for complex components

## Build and Deploy
- Development: `npm run dev` (runs on port 3000)
- Build: `npm run build`
- Preview: `npm run preview`
- Test: `npm run test`

## Important Notes
- This is a private package (not published to npm)
- Demo files prefixed with `demo` can be safely deleted
- The router uses code generation (`routeTree.gen.ts`)
- Follow the TanStack ecosystem patterns and conventions
