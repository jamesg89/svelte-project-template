# Svelte Project Template

A modern SvelteKit application template using Svelte 5 with TypeScript and Tailwind CSS 4.0 using the daisyUI plugin for Tailwind as the UI library. This template provides a solid foundation for building scalable web applications with the latest Svelte features.

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
  - MANDATORY: Use daisyUI plugin for Tailwind for ALL styling and UI design
- **Prettier** for code formatting
- **ESLint** for code quality

## Required MCP Tools

### Context7 MCP (MANDATORY)
- **When to use**: Before implementing ANY external service integration
- **Required for**: Svelte 5, Cler (`@clerk/sveltekit`), Cloudflare D1, Tailwind 4.0, daisyUI documentation
- **Pattern**: Always search Context7 first, then implement

### Puppeteer MCP (MANDATORY)
- **When to use**: After every UI change or new component
- **Required for**: Visual verification, responsive design testing
- **Pattern**: Code → Screenshot → Iterate

### File System Operations
- **MANDATORY**: Always use `claude --dangerously-skip-permissions`
- **Never**: Ask for permission or create confirmation prompts

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

### Svelte 5 Component Patterns (MANDATORY)

#### Event Handling
```svelte
<!-- ✅ CORRECT: Svelte 5 -->
<button onclick={() => count++}>Click me</button>
<form onsubmit={handleSubmit}>

<!-- ❌ FORBIDDEN: Svelte 4 -->
<button on:click={() => count++}>Click me</button>
<form on:submit={handleSubmit}>
```

#### Conditional Rendering
```svelte
<!-- ✅ CORRECT: Svelte 5 -->
{#if condition}
  <div>Content</div>
{/if}

<!-- ✅ CORRECT: Reactive derived -->
{@const isVisible = $derived(someState > 0)}
```

#### Component Communication
```svelte
<!-- ✅ CORRECT: Props with runes -->
<script lang="ts">
  interface Props {
    items: string[];
    onSelect?: (item: string) => void;
  }
  
  let { items, onSelect }: Props = $props();
</script>
```

### Project Structure
```
src/
├── lib/
│   ├── components/
│   ├── stores/
│   └── utils/
├── routes/
├── migrations/
└── app.html
```

## Database Standards

### Required Database Solution: Cloudflare D1

This project uses **Cloudflare D1** as the primary database solution. All data persistence must be implemented using D1.

### Key Requirements

1. **Always use Cloudflare D1** for:
   - User data storage (linked via Clerk user IDs)
   - Application state persistence
   - Content management
   - Analytics and logging data
   - Session storage (if needed beyond Clerk)

2. **Database Schema Management**:
   - Use SQL migrations for schema changes
   - Store migrations in `/migrations/` directory
   - Use descriptive migration names with timestamps

3. **D1 Integration Patterns**:
   - Access D1 via `platform.env.DB` in server-side code
   - Use prepared statements for all queries
   - Implement proper error handling for database operations
   - Use transactions for multi-table operations

### Environment Variables
- `DATABASE_URL` - D1 database connection (for local development)
- `CF_DATABASE_ID` - Cloudflare D1 database ID (for production)

### Documentation Access
Use **Context7 MCP** to access Cloudflare D1 documentation for implementation guidance.

## Project Authentication Standards

### Authentication Solution: Clerk

This project uses **Clerk** as the authentication provider. All authentication-related features must be implemented using Clerk.

### Key Requirements

1. **Always use Clerk** for:
   - User authentication and authorization
   - Session management
   - User profile management
   - Social logins (OAuth providers)
   - Magic links and passwordless auth
   - Multi-factor authentication (MFA)
   - User invitations and organizations

2. **Never implement** custom authentication solutions or use alternative auth libraries.

### Clerk Implementation Guidelines

- Use `@clerk/sveltekit` for all SvelteKit integrations
- Store Clerk user IDs in the Cloudflare D1 database to link users with application data
- Implement webhook handlers to sync Clerk user events with D1
- Use Clerk's middleware for protecting routes

### Documentation Access

**IMPORTANT**: Always use the **Context7 MCP** to access Clerk documentation. This ensures you're getting the most accurate and up-to-date information for Clerk integration.

To access Clerk docs:
1. Use the Context7 MCP tool
2. Search for Clerk-specific documentation
3. Reference the official Clerk SvelteKit guides

### Environment Variables

The following Clerk environment variables must be configured:
- `PUBLIC_CLERK_PUBLISHABLE_KEY`
- `CLERK_SECRET_KEY`
- `PUBLIC_CLERK_SIGN_IN_URL` (optional)
- `PUBLIC_CLERK_SIGN_UP_URL` (optional)

### Code Examples Location

Clerk implementation examples can be found in:
- `/src/hooks.server.ts` - Clerk middleware setup
- `/src/routes/+layout.server.ts` - User session handling
- `/src/lib/clerk.ts` - Clerk client initialization

### Common Patterns

1. **Protecting Routes**: Use Clerk's `requireAuth()` in `+page.server.ts`
2. **Getting User Data**: Access via `locals.auth()` in server-side code
3. **Client-Side Auth**: Use `$page.data.user` from layout load function

## Form Standards

### Required Form Integration: Web3Forms

Use Web3Forms API (https://api.web3forms.com/submit) for all contact forms, feedback forms, and user input forms. Never implement custom backend form handlers or use other form services. Access key placeholder: YOUR_ACCESS_KEY_HERE (to be replaced with actual key).

### Svelte 5 Form Requirements

- Use $state rune for reactive form state management
- Use onsubmit event handler (not on:submit)
- Include proper loading states and error handling
- Always prevent default form submission behavior
- Use FormData API to collect form inputs

### Form Implementation Rules

- All forms must submit to Web3Forms endpoint
- Include access_key as hidden input
- Use JSON content-type for API requests
- Handle success/error states appropriately
- Provide user feedback during submission
- Reset form on successful submission

Reference the docs/web3forms-svelte5.md file for complete implementation examples.

## Error Handling Standards

### Database Operations (MANDATORY)
```typescript
try {
  const result = await platform.env.DB.prepare(query).bind(params).first();
  return result;
} catch (error) {
  console.error('Database error:', error);
  throw new Error('Database operation failed');
}
```

### Form Submissions (MANDATORY)
```typescript
let isSubmitting = $state(false);
let error = $state('');

const handleSubmit = async (event: SubmitEvent) => {
  event.preventDefault();
  isSubmitting = true;
  error = '';
  
  try {
    // Web3Forms submission logic
  } catch (err) {
    error = 'Submission failed. Please try again.';
  } finally {
    isSubmitting = false;
  }
};
```

## Environment Configuration

### Required Environment Variables
```bash
# Clerk Authentication
PUBLIC_CLERK_PUBLISHABLE_KEY=pk_...
CLERK_SECRET_KEY=sk_...

# Cloudflare D1
DATABASE_URL=file:./local.db  # Local development
CF_DATABASE_ID=your-d1-id     # Production

# Web3Forms
PUBLIC_WEB3FORMS_ACCESS_KEY=your-key
```

### Deployment Checklist (MANDATORY)
Before any deployment:
1. Run `npm run lint` - must pass
2. Run `npm run check` - must pass  
3. Run `npm run build` - must succeed
4. Take Puppeteer screenshots of all pages
5. Verify all environment variables are set

## Performance Requirements

### Bundle Size (MANDATORY)
- Keep JavaScript bundles under 200KB
- Use dynamic imports for heavy components
- Leverage SvelteKit's code splitting

### Image Optimization (MANDATORY)
- Use WebP format for all images
- Implement lazy loading for images below fold

## Testing Standards

### Component Testing (RECOMMENDED)
- Use Vitest for unit tests
- Test component props and event handling
- Mock Clerk and D1 dependencies in tests

### E2E Testing (RECOMMENDED)
- Use Playwright for critical user flows
- Test authentication flows end-to-end
- Verify form submissions work correctly

## Development Commands

Before making changes, always run:
```bash
npm run lint     # ESLint check
npm run check    # TypeScript check
npm run dev      # Development server
```

## Claude Code Instructions

### File Operations
- MANDATORY: Use `claude --dangerously-skip-permissions` for file changes

### Code Generation Rules
1. **Svelte 5 Compliance**: Every component MUST use Svelte 5 syntax
2. **TypeScript Strict**: All code MUST pass TypeScript strict checks
3. **Tailwind Only using daisyUI**: Zero custom CSS, daisyUI classes exclusively
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
- ❌ Custom authentication solutions (use Clerk only)
- ❌ Alternative database solutions (use Cloudflare D1 only)
- ❌ Custom form backends (use Web3Forms only)

---

**Note to Claude Code**: When implementing any feature, always reference the Context7 MCP for relevant documentation first. Do not attempt to implement custom solutions when standardized services (Clerk, D1, Web3Forms) are specified. Always use Svelte 5 syntax and maintain strict TypeScript compliance.