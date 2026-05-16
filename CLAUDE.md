# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository contains Anthropic's collection of skills for Claude. Skills are folders of instructions, scripts, and resources that Claude loads dynamically to improve performance on specialized tasks. These skills range from creative applications (art, music, design) to technical tasks (testing web apps, MCP server generation) to enterprise workflows (communications, branding, etc.).

**Key References:**
- Skills standard: https://agentskills.io
- How to create custom skills: https://support.claude.com/en/articles/12512198-creating-custom-skills
- Using skills in Claude: https://support.claude.com/en/articles/12512180-using-skills-in-claude

## Repository Structure

```
skills/
├── skills/                          # All skill implementations
│   ├── algorithmic-art/            # Generative art creation
│   ├── brand-guidelines/           # Brand identity utilities
│   ├── canvas-design/              # Visual design creation
│   ├── claude-api/                 # Claude API documentation & examples
│   ├── doc-coauthoring/            # Document co-authoring workflows
│   ├── docx/                       # Word document processing (source-available)
│   ├── frontend-design/            # Frontend design patterns
│   ├── internal-comms/             # Internal communication templates
│   ├── mcp-builder/                # MCP server generation
│   ├── pdf/                        # PDF processing (source-available)
│   ├── pptx/                       # PowerPoint processing (source-available)
│   ├── skill-creator/              # Skill creation & optimization tools
│   ├── slack-gif-creator/          # Slack GIF generation
│   ├── theme-factory/              # Theme generation utilities
│   ├── web-artifacts-builder/      # Web app artifact building
│   ├── webapp-testing/             # Web app testing with Playwright
│   └── xlsx/                       # Excel processing (source-available)
├── spec/                           # Agent Skills specification
├── template/                       # Template skill for new creations
├── .claude-plugin/                 # Plugin configuration
│   └── marketplace.json            # Marketplace metadata
└── README.md                       # Main documentation
```

## Skill Structure

Each skill is a self-contained folder with a consistent structure:

### Essential Structure
Every skill must have:
- **SKILL.md** - The skill's instructions and metadata (see format below)

### Optional Supporting Files
- **scripts/** - Helper scripts (Python, JavaScript, shell, etc.)
- **assets/** - Images, templates, or reference materials
- **references/** - Documentation or reference files
- **LICENSE.txt** - License information for source-available skills

### SKILL.md Format

Each SKILL.md begins with YAML frontmatter:

```yaml
---
name: skill-name                    # Unique identifier (lowercase, hyphens)
description: Clear description...   # What the skill does and when to use it
license: Complete terms in LICENSE.txt  # Optional, for source-available skills
---
```

Followed by markdown content with:
- H1 title matching the skill name
- Detailed instructions for Claude on how to use the skill
- Guidelines, patterns, and best practices
- Examples or use cases
- Reference to supporting files when applicable

**Key Convention:** Instructions should be written for Claude to follow, not as user-facing documentation. Use imperative language ("Write", "Create", "Use") and explain the decision tree for when/how to use supporting tools.

## Skill Categories and Patterns

### Document Skills (docx, pdf, pptx, xlsx)
- Source-available (not open source)
- Production-ready implementations used by Claude
- Handle complex file format processing
- Located in separate folders with internal structure

### Example/Reference Skills (in marketplace.json under "example-skills")
- Apache 2.0 licensed (mostly open source)
- Demonstrate patterns and possibilities
- Include scripts, templates, or supporting assets
- Cover: creative (art, design, GIFs), technical (MCP, testing), communication

### API Documentation Skills (claude-api)
- Provide reference materials and code examples
- Support multiple languages (Python, TypeScript, Go, Ruby, PHP, Java)
- Include managed agents guidance
- Organized by language in subdirectories

## Development and Contribution Patterns

### Creating a New Skill

1. **Start with the template:** Copy `template/SKILL.md` as a starting point
2. **Name the skill:** Use lowercase with hyphens (e.g., `my-skill-name`)
3. **Write the SKILL.md:** 
   - Clear description (when Claude should use it)
   - Step-by-step instructions
   - Decision trees for complex workflows
   - Reference supporting scripts/files with `--help` guidance

4. **Add supporting files if needed:**
   - Scripts should be documented with `--help` flags
   - Scripts should be called as "black boxes" rather than read into context
   - Include examples in an `examples/` subfolder
   - Use `references/` for documentation

5. **Update marketplace.json:**
   - Add skill path to appropriate plugin (document-skills or example-skills)
   - This makes it discoverable in Claude Code and Claude.ai

### Skill Writing Best Practices

**Instructions should:**
- Be written for Claude to follow, not as user documentation
- Include decision trees for complex tasks
- Reference helper scripts with guidance to "run --help first"
- Explain WHY certain approaches are better (e.g., "use bundled scripts as black boxes")
- Include reconnaissance-then-action patterns for exploratory tasks
- Avoid overloading context by referencing rather than including large scripts

**Avoid:**
- Copying existing artists' work (copyright concerns)
- Overly generic instructions without context
- Instructions that would be better as helper scripts
- Assuming Claude has already used the skill before

### Testing Skills

While there's no formal test framework in this repository:
- Skills are validated by running them in Claude and evaluating results
- The `skill-creator` skill includes evaluation patterns: test prompts → run → analyze quantitative metrics → iterate
- For complex skills with scripts, write small example scripts in `examples/` that demonstrate correct usage

### Marketplace Configuration

The `.claude-plugin/marketplace.json` file defines three plugin collections:

1. **document-skills** - Production document processing (xlsx, docx, pptx, pdf)
2. **example-skills** - Reference implementations showing various patterns
3. **claude-api** - API documentation and code examples

When adding a new skill to either collection, update the `skills` array in the appropriate plugin object.

## Key Files and Their Roles

- **README.md** - Main entry point; explains what skills are and how to use them
- **spec/agent-skills-spec.md** - References the official specification at agentskills.io
- **.claude-plugin/marketplace.json** - Defines how skills are grouped and distributed
- **template/SKILL.md** - Starting template for new skills
- **THIRD_PARTY_NOTICES.md** - Licensing information for all skills

## Common Commands

```bash
# No build/test/lint automation exists in this repository
# Skills are validated through usage in Claude, not automated pipelines

# Git workflow for changes
git checkout -b feature/skill-name
# ... make changes ...
git add .
git commit -m "Add skill-name skill" 
git push -u origin feature/skill-name
# Create a pull request via GitHub

# To register locally for Claude Code
cd /path/to/skills
/plugin marketplace add local:/path/to/skills
```

## Git and Publishing

- Changes are published via pull requests to the main branch
- Skills are distributed through:
  - Claude Code plugin marketplace (registered via `.claude-plugin/`)
  - Claude.ai (pre-built skills available to paid plans)
  - Claude API (custom skills can be uploaded)
- No automated CI/CD pipeline; skills are validated through community and Anthropic review

## Important Conventions

1. **Skill Naming:** Use lowercase with hyphens (e.g., `skill-creator`, `web-artifacts-builder`)
2. **Context Preservation:** Keep instructions concise; reference supporting scripts rather than including them inline
3. **Script Usage:** Always recommend running `--help` first before using helper scripts
4. **Language:** Write instructions as directives for Claude ("Create", "Write", "Use") rather than suggestions
5. **Licensing:** Clearly indicate license type in SKILL.md (Apache 2.0, source-available, etc.)
6. **File Organization:** Group related files (examples, references, assets) in descriptive subdirectories

## Working with Complex Skills

For skills with significant supporting code (like skill-creator, mcp-builder, webapp-testing):
- Supporting code lives in `scripts/`, `references/`, or `agents/` subdirectories
- The SKILL.md should guide Claude to USE these scripts, not READ them
- Large Python/JS files are treated as "black boxes" invoked with CLI flags
- Include example files in `examples/` to show correct usage patterns

## Disclaimer

Skills in this repository are provided for demonstration and educational purposes. While some capabilities may be available in Claude, implementations may differ from what's shown in these skills. Always test skills thoroughly before relying on them for critical tasks.
