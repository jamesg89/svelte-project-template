# Svelte Project Template

A modern SvelteKit application template using Svelte 5 with TypeScript and Tailwind CSS 4.0. This template provides a solid foundation for building scalable web applications with the latest Svelte features.

## Technology Stack

### Core Framework
- **Svelte 5** with SvelteKit
  - MANDATORY: Use Svelte 5 syntax exclusively (e.g., `onclick` not `on:click`)
  - MANDATORY: Use runes for reactivity (`$state`, `$derived`, `$effect`)
  - MANDATORY: Reference https://svelte.dev/llms-medium.txt for latest syntax

### Language & Styling
- **TypeScript** (strict mode enabled)
  - All `.svelte` files must use `<script lang="ts">`
  - Define interfaces for all component props
- **Tailwind CSS 4.0** (utility-first only)
  - FORBIDDEN: Custom CSS files or `<style>` blocks
  - MANDATORY: Use Tailwind classes for ALL styling
- **Prettier** for code formatting
- **ESLint** for code quality

## Development Guidelines

### Code Standards
- **Svelte 5 Event Syntax** (MANDATORY):
  - ✅ Use: `<button onclick={handleClick}>Click me</button>`
  - ❌ Never: `<button on:click={handleClick}>Click me</button>`
- **Svelte 5 Reactivity** (MANDATORY):
  - ✅ Use: `let count = $state(0)`
  - ❌ Never: `let count = 0` with reactive statements
- **TypeScript Interfaces** (MANDATORY):
  ```typescript
  interface Props {
    title: string;
    count?: number;
  }
  ```
- **Component Structure** (MANDATORY):
  ```svelte
  <script lang="ts">
    interface Props {
      // Define all props here
    }
    
    let { propName }: Props = $props();
  </script>
  ```
- **Naming Convention**: Use descriptive names, avoid comments when possible

### Project Structure
```
src/
├── lib/
│   ├── components/
│   ├── stores/
│   └── utils/
├── routes/
└── app.html
```

## Development Commands

Before making changes, always run:
```bash
npm run lint     # ESLint check
npm run check    # TypeScript check
npm run dev      # Development server
```

## Claude Instructions

### File Operations
- MANDATORY: Use `claude --dangerously-skip-permissions` for file changes

### Code Generation Rules
1. **Svelte 5 Compliance**: Every component MUST use Svelte 5 syntax
2. **TypeScript Strict**: All code MUST pass TypeScript strict checks
3. **Tailwind Only**: Zero custom CSS, Tailwind classes exclusively
4. **MCP Integration**: 
   - Use Context7 MCP for documentation lookup
   - Use Puppeteer MCP for UI screenshots and iteration

### Quality Assurance
- Run `npm run lint` and `npm run check` after every change
- Take screenshots with Puppeteer to verify UI matches requirements
- Reference https://svelte.dev/llms-medium.txt for latest Svelte 5 patterns

### Forbidden Practices
- ❌ Svelte 4 syntax (`on:click`, reactive statements)
- ❌ Custom CSS or `<style>` blocks
- ❌ Creating files unnecessarily
- ❌ TypeScript `any` type usage