# figma-design-to-code-webinar

A focused React component library demonstrating the Figma → Code workflow using GitHub Copilot and the Obra design system.

## Project Structure

```text
src/
├── components/
│   ├── obra/            # Obra design system UI components (Figma-connected primitives)
│   └── common/          # Shared reusable components (composed higher-level components)
├── lib/
│   └── utils.ts         # cn() utility
├── index.css            # Global styles + CSS design tokens
└── main.tsx             # App entry point
```

## Commands

- **Storybook**: `npm run storybook` — View components at http://localhost:6006
- **Unit Tests**: `npm test`
- **Type Checking**: `npm run typecheck`
- **Figma Publish**: `npm run figma:publish` — Publish Code Connect mappings

## Coding Standards

- Language: TypeScript 5.x / React 18+
- No inline comments in `.tsx`/`.ts` files
- All styling via Tailwind CSS classes — no inline styles
- Every component must have a `.test.tsx` and `.stories.tsx`
- Use `cn()` from `@/lib/utils` for conditional class merging

### Component Architecture

Follow the **modlet pattern** — each component lives in its own folder:

```text
ComponentName/
├── ComponentName.tsx
├── ComponentName.test.tsx
├── ComponentName.stories.tsx
├── index.ts
├── types.ts        (optional, for complex types)
└── README.md       (optional)
```

- **Obra components** → `src/components/obra/` (Figma-connected primitives)
- **Common components** → `src/components/common/` (composed higher-level components)

### Shadcn UI

- Use Obra components from `src/components/obra/` wherever possible
- Install new shadcn primitives via `npx shadcn@latest add [component-name]` if a primitive is missing

### Import Alias

Use `@/` for all src-relative imports:

```ts
import { cn } from '@/lib/utils';
import { Button } from '@/components/obra/Button';
import { Avatar } from '@/components/obra/Avatar';
```

## Skills

Skills live in `.claude/skills/`. Before implementing any feature, review the table below and read the relevant skill file.

### Skill Execution Rules

When executing any skill that has a `steps/` folder:

1. Read `steps/00-todo-setup.md` first — before writing any code or creating any files
2. Copy the todo list exactly from that file using `manage_todo_list` — do NOT improvise
3. Mark each todo `in-progress` before starting it and `completed` immediately after finishing
4. Do not skip steps — every item in the canonical list must be completed or explicitly blocked

| Skill | Purpose | When to Use |
|-------|---------|-------------|
| `component-reuse` | Ensure existing UI components are reused before creating new ones | Before implementing any UI from Figma |
| `validate-implementation` | Validate implementations for runtime errors and API compliance | Before marking any feature complete |
| `figma-implement-component` | Implement React components from Figma designs | After component-reuse confirms no existing component |
| `figma-design-react` | Design React components from Figma files | When analyzing Figma designs to propose component architecture |
| `figma-component-sync` | Check React components against Figma design source | When reviewing implementations or auditing visual accuracy |
| `figma-connect-component` | Generate Figma Code Connect mapping for components | When linking React components to their Figma counterparts |
| `figma-connect-shadcn` | Connect shadcn/ui components to Figma | After adding shadcn components |
| `figma-explore` | Explore Figma files to discover pages and components | When you need to find component node IDs |
| `create-react-modlet` | Create React components following the modlet pattern | When creating any new component |
