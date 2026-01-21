---
name: notion-publisher
description: Publish markdown files to Notion using the Notion MCP, preserving folder hierarchy as nested pages. Use when the user wants to sync markdown docs to Notion, publish documentation to Notion, or mirror a folder structure in Notion. Triggers on "publish to Notion", "sync to Notion", "upload markdown to Notion".
---

# Notion Publisher

Publish markdown files to Notion using the Notion MCP, preserving folder structure as nested pages.

## Workflow

### 1. Identify Target

Ask the user for:
- **Source**: Which markdown file(s) or directory to publish
- **Destination**: The Notion page ID or URL where content should go

### 2. Mirror Folder Structure

When publishing a directory, create nested Notion pages matching the folder hierarchy:

```
docs/
├── roles/
│   └── jds/
│       └── engineer.md
```

Becomes:
```
Parent Page
└── roles (empty page)
    └── jds (empty page)
        └── engineer (page with content)
```

**Process:**
1. Read the directory structure
2. For each folder: create an empty Notion page as a child of its parent
3. For each `.md` file: create a Notion page with converted content

### 3. Convert Markdown to Notion

When creating pages from markdown:

1. **Title**: Use the first `# H1` heading, or filename if no H1
2. **Content**: Convert markdown elements to Notion blocks:
   - `# H1` → heading_1
   - `## H2` → heading_2
   - `### H3` → heading_3
   - Paragraphs → paragraph blocks
   - `- item` → bulleted_list_item
   - `1. item` → numbered_list_item
   - `` `code` `` → code annotation
   - `**bold**` → bold annotation
   - `*italic*` → italic annotation
   - `[text](url)` → link
   - ` ``` ` code blocks → code block
   - `> quote` → quote block
   - `---` → divider

### 4. Publish Sequence

For a directory:
1. Create folder pages first (depth-first), tracking page IDs
2. Then create content pages under their parent folder pages
3. Report URLs of created pages

For a single file:
1. Read the markdown content
2. Convert to Notion blocks
3. Create page under specified parent
4. Return the page URL

## Example Usage

User: "Publish docs/roles/jds to Notion page cea23274f41e4315ba41486f92385c64"

1. Read `docs/roles/jds/` directory structure
2. Create "jds" folder page (if publishing jds/ directly, or nested if publishing from higher level)
3. For each `.md` file in jds/:
   - Read content
   - Extract title from first H1
   - Convert body to Notion blocks
   - Create page under jds page
4. Return list of created page URLs
