# figma-design-to-code-webinar

> Project context and coding standards live in `AGENTS.md` at the repo root.
> Skills live in `.claude/skills/`.

## Skills

Before implementing any feature, read the relevant skill from `.claude/skills/`:

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
