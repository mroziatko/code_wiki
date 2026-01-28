# AI Agents Instructions

This document provides instructions and guidelines for AI agents (like GitHub Copilot, ChatGPT, Claude, etc.) when working with this codebase.

## Table of Contents
- [Project Overview](#project-overview)
- [Architecture](#architecture)
- [Development Workflow](#development-workflow)
- [Code Guidelines](#code-guidelines)
- [Testing Strategy](#testing-strategy)
- [Common Patterns](#common-patterns)
- [Troubleshooting](#troubleshooting)

## Project Overview

**Code Wiki** is a modern web application for creating and managing technical documentation and code wikis. It's built with cutting-edge React technologies to provide a fast, type-safe, and developer-friendly experience.

### Key Technologies
- **React 19.2.0**: Latest React with modern features
- **TanStack Router**: File-based routing system
- **TypeScript**: Full type safety across the codebase
- **Vite**: Fast build tool and development server
- **Vitest**: Unit testing framework
- **Testing Library**: React component testing

### Project Goals
1. Provide an intuitive wiki interface for code documentation
2. Maintain type safety throughout the application
3. Ensure fast performance and excellent UX
4. Keep the codebase maintainable and well-tested

## Architecture

### Directory Structure
```
code_wiki/
├── .github/
│   └── agents/
│       └── copilot-instructions.md
├── public/
├── src/
│   ├── routes/          # File-based routing (TanStack Router)
│   ├── components/      # Reusable React components
│   ├── data/           # Data management utilities
│   ├── App.css         # App-specific styles
│   ├── styles.css      # Global styles
│   └── router.tsx      # Router configuration
├── package.json
├── vite.config.ts
├── tsconfig.json
└── README.md
```

### Routing System
The project uses TanStack Router's file-based routing:
- Routes are defined as files in `src/routes/`
- The router automatically generates `routeTree.gen.ts`
- Layout is managed in `src/routes/__root.tsx`

### Component Organization
- Keep components small and focused on a single responsibility
- Co-locate tests with components (e.g., `Button.tsx` and `Button.test.tsx`)
- Group related components in subdirectories
- Export public APIs through index files

## Development Workflow

### Setting Up
```bash
# Install dependencies
npm install

# Start development server (port 3000)
npm run dev

# Run tests
npm run test

# Build for production
npm run build
```

### Making Changes
1. Create or modify components in `src/components/`
2. Add routes in `src/routes/` for new pages
3. Write tests alongside your code
4. Run tests to ensure nothing breaks
5. Build to verify production readiness

### Git Workflow
- Create feature branches from main
- Write descriptive commit messages
- Ensure tests pass before committing
- Keep commits focused and atomic

## Code Guidelines

### TypeScript Best Practices
```typescript
// ✅ Good: Explicit types for props
interface ButtonProps {
  label: string;
  onClick: () => void;
  disabled?: boolean;
}

export function Button({ label, onClick, disabled = false }: ButtonProps) {
  return <button onClick={onClick} disabled={disabled}>{label}</button>;
}

// ❌ Avoid: Using 'any' or implicit types
function Button(props: any) { ... }
```

### Component Patterns
```typescript
// ✅ Good: Functional components with hooks
import { useState } from 'react';

interface CounterProps {
  initialValue?: number;
}

export function Counter({ initialValue = 0 }: CounterProps) {
  const [count, setCount] = useState(initialValue);
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

// ❌ Avoid: Class components (unless necessary)
class Counter extends React.Component { ... }
```

### Styling Approach
```css
/* Prefer semantic class names */
.wiki-article { }
.wiki-article__title { }
.wiki-article__content { }

/* Avoid inline styles unless dynamic */
<div style={{ color: 'red' }}> ❌
```

### File Naming
- Components: PascalCase (e.g., `WikiArticle.tsx`)
- Utilities: camelCase (e.g., `formatDate.ts`)
- Tests: Same as file with `.test.` suffix (e.g., `WikiArticle.test.tsx`)
- Styles: kebab-case for CSS files (e.g., `wiki-article.css`)

## Testing Strategy

### Writing Tests
```typescript
import { render, screen } from '@testing-library/react';
import { Button } from './Button';

describe('Button', () => {
  it('renders with label', () => {
    render(<Button label="Click me" onClick={() => {}} />);
    expect(screen.getByText('Click me')).toBeInTheDocument();
  });

  it('calls onClick when clicked', () => {
    const handleClick = vi.fn();
    render(<Button label="Click" onClick={handleClick} />);
    
    screen.getByText('Click').click();
    expect(handleClick).toHaveBeenCalledTimes(1);
  });
});
```

### Test Coverage Goals
- Test all public component APIs
- Test user interactions and state changes
- Test error states and edge cases
- Avoid testing implementation details

### Running Tests
```bash
# Run all tests
npm run test

# Run tests in watch mode
npm run test -- --watch

# Run tests with coverage
npm run test -- --coverage
```

## Common Patterns

### Creating a New Route
```typescript
// src/routes/about.tsx
import { createFileRoute } from '@tanstack/react-router';

export const Route = createFileRoute('/about')({
  component: AboutComponent,
});

function AboutComponent() {
  return (
    <div>
      <h1>About</h1>
      <p>Welcome to Code Wiki</p>
    </div>
  );
}
```

### Data Loading with Router
```typescript
export const Route = createFileRoute('/articles/$id')({
  loader: async ({ params }) => {
    const article = await fetchArticle(params.id);
    return { article };
  },
  component: ArticleComponent,
});

function ArticleComponent() {
  const { article } = Route.useLoaderData();
  return <div>{article.title}</div>;
}
```

### Navigation
```typescript
import { Link } from '@tanstack/react-router';

function Navigation() {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
      <Link to="/articles">Articles</Link>
    </nav>
  );
}
```

## Troubleshooting

### Common Issues

#### TypeScript Errors
- Ensure all dependencies are installed: `npm install`
- Check `tsconfig.json` for proper configuration
- Verify TypeScript version matches project requirements

#### Router Issues
- Check that route files follow TanStack Router conventions
- Verify `routeTree.gen.ts` is generated (auto-generated on dev/build)
- Ensure route file names match the desired URL structure

#### Test Failures
- Run tests in isolation to identify specific failures
- Check for missing test dependencies
- Verify test environment setup (jsdom)

#### Build Errors
- Clear build cache: `rm -rf dist`
- Check for circular dependencies
- Verify all imports are valid

### Getting Help
1. Check the project README.md
2. Review TanStack Router documentation: https://tanstack.com/router
3. Check React documentation: https://react.dev
4. Review TypeScript documentation: https://www.typescriptlang.org/docs

## AI Agent Specific Notes

### When Suggesting Changes
1. **Understand the context**: Review related files before suggesting changes
2. **Maintain consistency**: Follow existing patterns in the codebase
3. **Consider type safety**: Ensure TypeScript types are correct and complete
4. **Think about testing**: Suggest tests for new functionality
5. **Be minimal**: Make the smallest change that achieves the goal

### Code Review Checklist
- [ ] TypeScript types are correct and complete
- [ ] Component props are properly typed
- [ ] Tests are included for new functionality
- [ ] Code follows existing patterns
- [ ] No console.log or debug statements left behind
- [ ] Imports are organized and unused ones removed
- [ ] Error handling is appropriate
- [ ] Performance considerations are addressed

### Best Practices for AI Agents
- Ask clarifying questions if requirements are unclear
- Suggest alternative approaches when appropriate
- Explain trade-offs in technical decisions
- Provide examples and documentation links
- Consider accessibility and user experience
- Think about edge cases and error states

---

**Last Updated**: January 2026

For more specific GitHub Copilot instructions, see `.github/agents/copilot-instructions.md`
