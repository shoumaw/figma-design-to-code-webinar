# Step 6: Create Stories for Each Variant

Before starting: Mark Step 6 as `in-progress` in todo list.

Create `{ComponentName}.stories.tsx` with a story for **every Figma variant**:

## Template

```tsx
import type { Meta, StoryObj } from '@storybook/react';
import { ComponentName } from './ComponentName';

const meta: Meta<typeof ComponentName> = {
  component: ComponentName,
  title: 'Common/ComponentName',
  tags: ['autodocs'],
  parameters: {
    design: {
      type: 'figma',
      url: 'https://figma.com/design/...?node-id=...', // From design-context.md
    },
  },
};

export default meta;
type Story = StoryObj<typeof ComponentName>;

// Default state (matches Figma default)
export const Default: Story = {
  args: {
    children: 'Button Label',
  },
};

// Size variants
export const Small: Story = {
  args: {
    size: 'sm',
    children: 'Small Button',
  },
};

export const Medium: Story = {
  args: {
    size: 'md',
    children: 'Medium Button',
  },
};

export const Large: Story = {
  args: {
    size: 'lg',
    children: 'Large Button',
  },
};

// Type variants
export const Primary: Story = {
  args: {
    variant: 'primary',
    children: 'Primary',
  },
};

export const Secondary: Story = {
  args: {
    variant: 'secondary',
    children: 'Secondary',
  },
};

// Boolean properties
export const WithIcon: Story = {
  args: {
    icon: <span>★</span>,
    children: 'With Icon',
  },
};

export const Disabled: Story = {
  args: {
    disabled: true,
    children: 'Disabled',
  },
};

// Responsive stories (if Figma has responsive designs)
export const Mobile: Story = {
  args: {
    children: 'Mobile View',
  },
  parameters: {
    viewport: { defaultViewport: 'mobile1' },
  },
};
```

## Required: Figma Comparison Story

**Every** stories file MUST include a `AllVariants` story that renders all variant combinations in a grid that mirrors how the component set is laid out in Figma. This enables direct visual comparison between the Figma design and the implementation.

Layout rules:
- Group rows by the **primary variant axis** (e.g. `variant` or `type`)
- Group columns by the **secondary variant axis** (e.g. `size` or `state`)
- Add a header row and header column with labels so each cell is identifiable
- Use consistent spacing (`gap-3` or `gap-4`) and align items with `items-center`
- Label rows/columns with `<span className="text-xs text-gray-400 w-20">` style text

```tsx
export const AllVariants: Story = {
  name: 'All Variants',
  render: () => {
    const variants = ['primary', 'secondary', 'outline', 'ghost', 'destructive'] as const;
    const sizes = ['lg', 'md', 'sm', 'xs'] as const;

    return (
      <div className="flex flex-col gap-4 p-4">
        {/* Header row */}
        <div className="flex items-center gap-3">
          <span className="w-24 text-xs text-gray-400" />
          {sizes.map((size) => (
            <span key={size} className="w-24 text-center text-xs text-gray-400">
              {size}
            </span>
          ))}
        </div>
        {/* Variant rows */}
        {variants.map((variant) => (
          <div key={variant} className="flex items-center gap-3">
            <span className="w-24 text-xs text-gray-400">{variant}</span>
            {sizes.map((size) => (
              <div key={size} className="flex w-24 justify-center">
                <ComponentName variant={variant} size={size}>
                  Label
                </ComponentName>
              </div>
            ))}
          </div>
        ))}
      </div>
    );
  },
};
```

Adapt the axes and labels to match the actual component's props. If the component has boolean props (e.g. `disabled`, `withIcon`), add additional rows for those states below the main grid.

After completion: Mark Step 6 as `completed` in todo list.
