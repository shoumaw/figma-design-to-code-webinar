# Component Library — src/

This directory contains the React component library for the Figma Design to Code webinar.

## Directory Structure

```
src/
├── components/
│   ├── obra/          # Obra UI components (Figma-connected primitives)
│   └── common/        # Reusable composed components
├── lib/
│   └── utils.ts       # cn() utility (clsx + tailwind-merge)
├── index.css          # Global styles + CSS design tokens
└── main.tsx           # App entry point
```

## Naming Conventions

- **PascalCase** for component folders: `Button/`, `Avatar/`
- **kebab-case** for grouping/utility folders (non-components)
- **lowercase** for standard folders: `components/`, `lib/`

## Component Pattern (Modlet)

Each component follows the modlet pattern:

```
ComponentName/
├── ComponentName.tsx
├── ComponentName.test.tsx
├── ComponentName.stories.tsx
├── index.ts
└── types.ts           (optional)
```

## Import Rules

```typescript
import { cn } from '@/lib/utils';
import { Button } from '@/components/obra/Button';
import { Avatar } from '@/components/obra/Avatar';
import { Dialog, DialogHeader } from '@/components/obra/Dialog';
```

## Styling

Use Tailwind CSS classes. Put custom styles in external CSS files, not inline.

```tsx
<div className="flex items-center gap-4 p-4">
```

## Testing

```typescript
import { describe, it, expect, vi } from 'vitest';
import { render, screen } from '@testing-library/react';
import { ComponentName } from './ComponentName';

describe('ComponentName', () => {
  it('renders correctly', () => {
    render(<ComponentName />);
    expect(screen.getByText('Expected')).toBeInTheDocument();
  });
});
```

Run tests: `npm test`

## Storybook

```typescript
import type { Meta, StoryObj } from '@storybook/react';
import { ComponentName } from './ComponentName';

const meta: Meta<typeof ComponentName> = {
  component: ComponentName,
  title: 'Obra/ComponentName',
  tags: ['autodocs'],
  parameters: {
    design: {
      type: 'figma',
      url: 'https://www.figma.com/design/...',
    },
  },
};

export default meta;
type Story = StoryObj<typeof ComponentName>;

export const Default: Story = {
  args: {},
};
```

Run Storybook: `npm run storybook`
