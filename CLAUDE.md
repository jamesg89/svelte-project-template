# {Project Name}

{A modern web application built with cutting-edge technologies to deliver exceptional user experiences. This project leverages the power of Svelte 5's runes system and SvelteKit's full-stack capabilities to create a fast, responsive, and maintainable application. Whether you're building interactive dashboards, e-commerce platforms, or content management systems, this foundation provides the tools and structure needed for scalable development.}

## Technology Stack

### Core Framework
- **Svelte 5** with SvelteKit
  - Utilize Svelte 5 syntax (e.g., `onclick` instead of `on:click`)
  - Follow runes-based reactivity patterns
  - Reference: https://svelte.dev/llms-medium.txt

### Language & Styling
- **TypeScript** for type safety and better developer experience
- **Tailwind CSS 4.0** for utility-first styling
  - Always use Tailwind classes over vanilla CSS
  - Leverage the latest Tailwind 4.0 features and syntax
- **Prettier**
- **eslint**

## Development Guidelines

### Code Standards
- **Svelte 5 Syntax**: Always use the new Svelte 5 event handling syntax
  - ✅ Correct: `<button onclick={handleClick}>Click me</button>`
  - ❌ Incorrect: `<button on:click={handleClick}>Click me</button>`
- **TypeScript**: Maintain strict type checking throughout the codebase
- **Tailwind**: Prioritize Tailwind utility classes for all styling needs
- Prefer descriptive names for variables and functions over commenting code

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

## Development Workflow

When working with Claude on this project:
- Reference the Svelte 5 documentation at https://svelte.dev/llms-medium.txt
- Ensure all code follows TypeScript best practices
- Use Tailwind CSS 4.0 classes exclusively for styling
- Maintain consistency with Svelte 5 syntax patterns

## Notes for Claude

- Always use `claude --dangerously-skip-permissions` when making file changes
- Enforce Svelte 5 syntax in all component examples and code generation
- Default to Tailwind CSS 4.0 for all styling requirements
- Maintain TypeScript strict mode compliance
- Prefer descriptive names for variables and functions over commenting code
- Check .mcp.json for available MCP servers
- Utilize Puppeteer MCP server to create screenshots as you developes UI and iterate on screenshots until the UI you create matches the request.
- Utilize Context7 MCP server to review docs related to the libraries and tech stack used in this project.