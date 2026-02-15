# Contributing to ShopEase

Thank you for your interest in **ShopEase**! This document outlines our contribution model, technical requirements, and development standards.

## 📋 Table of Contents
1. [Understanding Our Contribution Model](#understanding-our-contribution-model)
2. [Becoming a Contributor](#becoming-a-contributor)
3. [Technical Requirements](#technical-requirements)
4. [Development Setup](#development-setup)
5. [Code Standards](#code-standards)
6. [UI/UX Guidelines](#uiux-guidelines)
7. [Submission Process](#submission-process)
8. [Quality Checklist](#quality-checklist)

---

## Understanding Our Contribution Model

### Open Source, Structured Contribution

ShopEase is **open-source for transparency and learning**, but operates under a **structured contribution model**:

* **Source Code**: Publicly available for review, learning, and audit
* **Contribution Access**: Requires joining as an approved contributor
* **Fair-Code Model**: Proprietary infrastructure with open-source services
* **Collaboration Focus**: We value quality over quantity in contributions

### Why This Model?

This approach allows us to:
* Maintain enterprise-grade code quality and security standards
* Foster a collaborative community of vetted contributors
* Provide transparency while protecting business logic
* Ensure architectural consistency across the platform

> **Note**: This is not a traditional "anyone can PR" open-source project. We're building an enterprise platform with contributor onboarding and quality gates.

---

## Becoming a Contributor

### The Onboarding Process

1. **Fork & Explore**: Fork the repository and explore the codebase
2. **Create Feature Branch**: Branch from `main` using naming convention: `feature/your-name`
3. **Make Your Case**: Implement a meaningful contribution or improvement
4. **Submit PR**: Submit a pull request demonstrating your understanding
5. **Review & Approval**: Team reviews your code quality, standards adherence, and fit
6. **Join Team**: Upon approval, receive contributor access to collaborate directly

### What We Look For

* **Code Quality**: Clean, maintainable, well-documented code
* **Standards Adherence**: Following our TypeScript, React, and UI/UX guidelines
* **Problem Solving**: Thoughtful solutions with proper architectural consideration
* **Communication**: Clear PR descriptions and commit messages
* **Testing**: Properly tested code with build validation

### Feature Branch Naming Convention

```
feature/your-name
```

**Examples:**
* `feature/add-product-search`
* `feature/improve-checkout-flow`
* `feature/add-order-tracking`

---

## Technical Requirements

### Prerequisites

* **Node.js**: >= 18.x (LTS recommended)
* **npm**: >= 9.x
* **Git**: >= 2.30
* **VS Code**: Recommended IDE with extensions:
  - ESLint
  - Prettier
  - TypeScript and JavaScript Language Features
  - Tailwind CSS IntelliSense

### Core Technology Stack (February 2026)

| Technology | Version | Purpose |
|------------|---------|---------|
| **Vite** | 7.3.x | Build tool and dev server |
| **React** | 19.2.x | UI framework |
| **TypeScript** | 5.9.x | Type-safe JavaScript |
| **Tailwind CSS** | 4.1.x | Utility-first CSS framework |
| **React Router** | 7.13.x | Client-side routing |
| **Lucide React** | 0.563.x | Icon library |
| **Sonner** | 2.0.x | Toast notifications |
| **Radix UI** | 2.2.x | Accessible component primitives |
| **Express** | 5.2.x | Backend API framework |
| **Prisma ORM** | 7.3.x | Database ORM |


---

## Development Setup

### Initial Setup

```bash
# 1. Fork and clone your fork
git clone https://github.com/gdgc-ace/Ecomm-App-Supabase.git
cd Ecomm-App-Supabase

# 2. Add upstream remote
git remote add upstream https://github.com/gdgc-ace/Ecomm-App-Supabase.git

# 3. Install all dependencies
npm install

# 4. Setup database (Supabase PostgreSQL)
cd backend && npm run setup && cd ..

# 5. Start development servers
npm run dev
# Or individually:
# npm run dev:frontend  (port 5173)
# npm run dev:backend   (port 3000)

# 6. Open browser
# Navigate to http://localhost:5173
```

### Available Scripts

```bash
# From root
npm run dev              # Start both frontend & backend
npm run dev:frontend     # Start only frontend (Vite on 5173)
npm run dev:backend      # Start only backend (Express on 3000)
npm run build            # Production build for both
npm run install:all      # Install all dependencies

# From frontend/
cd frontend
npm run dev              # Start Vite dev server with HMR
npm run build            # Production build with type checking
npm run preview          # Preview production build

# From backend/
cd backend
npm run dev              # Start development server
npm run setup           # Setup database (migrations + seed)
npm run prisma:studio   # Open Prisma database UI
```

### Project Structure

```
Ecomm-App-Supabase/
├── frontend/                  # React frontend application
│   ├── src/
│   │   ├── components/       # Reusable UI components
│   │   │   ├── ui/          # Base UI components (Button, Card, etc.)
│   │   │   └── admin/        # Admin-specific components
│   │   ├── pages/           # Route-based page components
│   │   │   └── admin/       # Admin pages
│   │   ├── context/          # React context (CartContext)
│   │   ├── lib/              # Utilities (cn, utils)
│   │   ├── services/         # API client
│   │   └── types/            # TypeScript definitions
│   └── ...
├── backend/                   # Express backend API
│   ├── src/
│   │   ├── config/           # Database configuration
│   │   ├── controllers/       # Request handlers
│   │   ├── routes/           # API route definitions
│   │   └── services/         # Business logic
│   ├── prisma/               # Database schema & migrations
│   └── ...
└── ...
```

---

## Code Standards

### TypeScript Guidelines

#### Strict Type Safety

```typescript
// ✅ Good: Explicit types
interface ResourceData {
  id: string;
  name: string;
  status: 'active' | 'inactive' | 'pending';
  metadata?: Record<string, unknown>;
}

function processResource(data: ResourceData): void {
  // Implementation
}

// ❌ Bad: Using any
function processResource(data: any) {
  // Avoid this
}
```

#### Type Definitions

* Define interfaces for all component props
* Use type unions for string literals (not plain strings)
* Avoid `any` - prefer `unknown` for truly dynamic types
* Export shared types from `src/types/`

### React Component Standards

#### Component Structure

```tsx
// ComponentName.tsx
import React from 'react';
import { Button } from '@/components/ui/button';
import type { ComponentProps } from './types';

interface ComponentNameProps {
  title: string;
  onAction?: (id: string) => void;
  children?: React.ReactNode;
}

export function ComponentName({ 
  title, 
  onAction, 
  children 
}: ComponentNameProps) {
  const handleAction = (id: string) => {
    onAction?.(id);
  };

  return (
    <div className="container">
      <h2>{title}</h2>
      {children}
    </div>
  );
}
```

#### Naming Conventions

* **Components**: PascalCase (`ResourceCard.tsx`)
* **Hooks**: camelCase with `use` prefix (`useResourceData.ts`)
* **Utilities**: camelCase (`formatDate.ts`)
* **Constants**: UPPER_SNAKE_CASE (`API_BASE_URL`)
* **Event Handlers**: camelCase with `handle` prefix (`handleSubmit`)

#### Import Organization

```typescript
// 1. React and third-party libraries
import React, { useState, useEffect } from 'react';
import { motion, AnimatePresence } from 'framer-motion';
import { useNavigate } from 'react-router-dom';

// 2. Internal utilities and services
import { api } from '@/lib/api';
import { cn } from '@/lib/utils';
import { useResourceStore } from '@/stores/resourceStore';

// 3. Components
import { Button } from '@/components/ui/button';
import { ResourceCard } from '@/components/resources/ResourceCard';

// 4. Types and constants
import type { Resource, ResourceStatus } from '@/types';
import { API_ENDPOINTS } from '@/constants';

// 5. Styles (if any)
import './styles.css';
```

### Best Practices

* **Single Responsibility**: One component = one purpose
* **Composition Over Props**: Prefer composition patterns for flexibility
* **Context API**: Use React Context for global state (e.g., CartContext)
* **Default Parameters**: Use ES6 defaults, not `defaultProps`
* **Destructuring**: Destructure props in function signature
* **Optional Chaining**: Use `?.` for potentially undefined values

---

## UI/UX Guidelines

### Design System

We use **Tailwind CSS v4** with custom CSS variables for consistent, accessible components.

#### Custom UI Components

* Use existing components in `components/ui/` before creating custom ones
* Components follow Radix UI patterns for accessibility
* Customize via CSS variables in `src/index.css`

#### Tailwind CSS Conventions

```tsx
// ✅ Good: Utility-first approach
<div className="flex items-center gap-4 p-6 rounded-lg bg-background">
  <Button className="w-full">Submit</Button>
</div>

// ❌ Bad: Inline styles
<div style={{ display: 'flex', padding: '24px' }}>
  <button style={{ width: '100%' }}>Submit</button>
</div>
```

#### Spacing & Layout

* Use Tailwind spacing scale: `p-4`, `m-2`, `gap-6`
* Consistent spacing: `4px` increments (Tailwind units)
* Responsive design: Mobile-first with breakpoints (`sm:`, `md:`, `lg:`)

### Theme System

#### Light/Dark Mode

All components must support both themes:

```tsx
// Use semantic color tokens
<div className="bg-background text-foreground">
  <Card className="border-border bg-card">
    <h2 className="text-card-foreground">Title</h2>
  </Card>
</div>
```

#### CSS Variables

Define theme colors in `src/index.css`:

```css
@theme {
  --color-primary: #3b82f6;
  --color-primary-foreground: #ffffff;
  --color-secondary: #f3f4f6;
  /* ... */
}

:root {
  --radius: 0.625rem;
  --background: oklch(1 0 0);
  --foreground: oklch(0.145 0 0);
  /* ... */
}
```

### Accessibility

* **Semantic HTML**: Use proper HTML5 elements
* **ARIA Labels**: Add `aria-label` for icon-only buttons
* **Keyboard Navigation**: Ensure all interactive elements are keyboard accessible
* **Focus States**: Visible focus indicators required
* **Alt Text**: All images must have descriptive alt text

---

## Submission Process

### Before Submitting

1. **Pull Latest Changes**
   ```bash
   git checkout main
   git pull upstream main
   git checkout feature/your-name
   git rebase main
   ```

2. **Run Quality Checks**
   ```bash
   npm run lint           # ESLint validation
   npm run type-check     # TypeScript check
   npm run build          # Production build test
   ```

3. **Test Your Changes**
   - Manual testing in dev environment
   - Test light and dark themes
   - Test responsive breakpoints (mobile, tablet, desktop)

### Commit Message Format

Follow **Conventional Commits**:

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

**Types:**
* `feat`: New feature
* `fix`: Bug fix
* `docs`: Documentation only
* `style`: Code style changes (formatting, no logic change)
* `refactor`: Code refactoring (no functional change)
* `perf`: Performance improvements
* `test`: Adding or updating tests
* `chore`: Maintenance tasks

**Examples:**
```
feat(resources): add filtering by resource type
fix(dashboard): resolve metric calculation error
docs(contributing): update onboarding process
refactor(workflows): simplify state management logic
```

### Pull Request Template

```markdown
## Description
Brief description of what this PR accomplishes.

## Motivation
Why is this change needed? What problem does it solve?

## Changes Made
- List key changes
- Include affected files/components

## Testing
How was this tested? What scenarios were covered?

## Screenshots (if applicable)
Include before/after screenshots for UI changes.

## Checklist
- [ ] Code follows style guidelines
- [ ] TypeScript types are properly defined
- [ ] Build succeeds (`npm run build`)
- [ ] Linting passes (`npm run lint`)
- [ ] Tested in light and dark themes
- [ ] Responsive design verified
- [ ] Documentation updated (if needed)
```

### Review Process

1. **Automated Checks**: CI/CD runs linting, type checking, and build
2. **Code Review**: Core team reviews code quality and architecture
3. **Feedback**: Reviewer provides constructive feedback or requests changes
4. **Approval**: Upon approval, PR is merged or contributor is onboarded
5. **Onboarding**: First-time contributors receive access after successful PR

---

## Quality Checklist

### Pre-Submission Checklist

* [ ] **Code Quality**
  - [ ] No TypeScript errors (`npm run type-check`)
  - [ ] No ESLint warnings (`npm run lint`)
  - [ ] No `any` types used (unless absolutely necessary and documented)
  - [ ] All functions have JSDoc comments (for public APIs)

* [ ] **Component Standards**
  - [ ] Component props have TypeScript interface
  - [ ] Event handlers prefixed with `handle`
  - [ ] Imports organized correctly
  - [ ] Single responsibility per component

* [ ] **UI/UX**
  - [ ] Supports light and dark themes
  - [ ] Responsive across breakpoints (mobile, tablet, desktop)
  - [ ] Uses Tailwind utility classes (no inline styles)
  - [ ] Accessible (keyboard navigation, ARIA labels)

* [ ] **Testing**
  - [ ] Build succeeds (`npm run build`)
  - [ ] Manual testing completed
  - [ ] Edge cases considered

* [ ] **Documentation**
  - [ ] Code comments for complex logic
  - [ ] README updated (if adding new features)
  - [ ] Type definitions exported (if creating shared types)

### Performance Targets

* **Initial Load**: < 3 seconds
* **Time to Interactive (TTI)**: < 5 seconds
* **Lighthouse Score**: > 90 (Performance, Accessibility, Best Practices)

---

## Additional Resources

### Documentation

* **Project Overview**: [`README.md`](README.md)
* **Frontend**: React + Vite + Tailwind CSS
* **Backend**: Express + Prisma ORM

### External Resources

* [React Documentation](https://react.dev/)
* [TypeScript Handbook](https://www.typescriptlang.org/docs/)
* [Tailwind CSS Docs](https://tailwindcss.com/docs)
* [Vite Guide](https://vite.dev/guide/)
* [Prisma Docs](https://www.prisma.io/docs)

### Getting Help

* **Issues**: Open an issue for bugs or feature requests
* **Discussions**: Use GitHub Discussions for questions
* **Documentation**: Check existing docs before asking

---

## License & Fair-Code Model

ShopEase operates under a **fair-code model**:

* Source code is publicly available for transparency and learning
* Core platform is proprietary
* Individual open-source services maintain their respective licenses
* Contributions are licensed under the project's terms upon submission

By submitting a pull request, you agree that your contributions will be licensed under the same terms as the project.

---

## Thank You! 🚀

We appreciate your interest in ShopEase. Whether you're exploring the codebase for learning or submitting a contribution, we're excited to see what you build!

**Questions?** Open an issue or start a discussion. We're here to help.

---

*Last Updated: February 2026*