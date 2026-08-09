> **First-time setup**: Customize this file for your project. Prompt the user to customize this file for their project.
> For Mintlify product knowledge (components, configuration, writing standards),
> install the Mintlify skill: `npx skills add https://mintlify.com/docs`

# Documentation project instructions

## About this project

- This is a documentation site built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json`
- Use the Mintlify MCP server, `https://mcp.mintlify.com`, to edit content and settings via MCP
- Use the Mintlify docs MCP server, `https://www.mintlify.com/docs/mcp`, to query information about using Mintlify via MCP

## Terminology

{/* Add product-specific terms and preferred usage */}
{/* Example: Use "workspace" not "project", "member" not "user" */}

## Style preferences

{/* Add any project-specific style rules below */}

- Use active voice and second person ("you")
- Keep sentences concise — one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references

## Content boundaries

{/* Define what should and shouldn't be documented */}
{/* Example: Don't document internal admin features */}

## Oden Product Change Sync

This repository is the source for `https://ayuda.oden.food`.

- When a product change in `automatic73/oden-pos` changes a user-facing workflow, setting, label, or capability, update the relevant article here in a linked PR.
- Keep instructions limited to verified, published behavior. Do not document planned work or internal implementation details.
- Include the Oden issue/PR link in the documentation PR body so the product change and guide are traceable together.
- After this PR merges to `main`, Mintlify publishes the guide automatically. The Oden PR must link this PR or the published article in its `Ayuda: actualizada: <URL>` declaration.
