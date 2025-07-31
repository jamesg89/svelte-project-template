# Svelte Project Template

This Project Template includes Typescript, Cloudflare Workers config, and standard Claude Code instructions so that you can spin up a new project in no time.

## Starting a new project with this template

1. Run the following command locally to copy this Project template into a new cloudflare project.
    npm create cloudflare@latest -- --template https://github.com/jamesg89/svelte-project-template.git

2. Update any AI instructions you plan to customize for the specific project
    Recommended files:

    - claude.md - Any coding best practices, project definition, tools and resources claude should use. By default has some generice coding practices and tools I generally use for projects

    - .mcp.json - add any special MCP's you might need for new project. By default:
        + server-sequential-thinking - force Claude to think harder
        + server-puppeteer - so Claude can take screenshots and iterate to make more accurate designs
        + context7 - Customize this to add documentation for any libraries/etc for added context for Claude
    
3. Deploy to Cloudflare
    npx wrangler dev/npx wrangler deploy

4. Start coding with Claude
    claude

## Recommended Extra Steps

Before starting to code, chat with Gemini or Claude about the project at a high level, and once satisfied, task AI to create a PRD file. Open claude code in the project with the new PRD and ask Claude Code if it has any questions about the PRD, refine based on response. Once satisfied, ask Claude Code to generate TASKS.md based on the PRD, and start tasking.

## Resources

https://docs.anthropic.com/en/docs/claude-code/overview

https://www.anthropic.com/engineering/claude-code-best-practices
