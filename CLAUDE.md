# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a curated collection of Claude skills for the Agent Skills standard. Skills are reusable instruction sets that enhance Claude's capabilities for specific tasks. The repository contains 33+ skills organized into 10 plugin collections via the Claude Code marketplace (`rickysanch12-skills`).

## Directory Structure

```
skills/
├── [skill-name]/
│   ├── SKILL.md          # Required: Frontmatter with name/description + instructions
│   └── [supporting files]
├── docx/, pptx/, xlsx/   # Source-available document processing skills
├── pdf/                  # PDF handling skill
├── template/             # Template for creating new skills
spec/                     # Agent Skills specification reference
.claude-plugin/           # Marketplace configuration
```

## Skill Format

Every skill folder must contain a `SKILL.md` file with:
- **YAML Frontmatter**: `name` (unique identifier, lowercase with hyphens) and `description` (when Claude should use it)
- **Markdown Content**: Instructions, examples, and guidelines Claude follows
- No other markup or fields required

Example:
```markdown
---
name: my-skill-name
description: Explain what this skill does and when to trigger it
---

# My Skill Name

[Instructions for Claude...]
```

## Plugin Collections

Skills are grouped in `.claude-plugin/marketplace.json` into collections:
- **document-skills**: docx, pptx, xlsx, pdf
- **example-skills**: algorithmic-art, brand-guidelines, canvas-design, etc.
- **development-tools**: git, code-formatter, api-client-generator, testing, docs, migrations, environment setup
- **code-quality**: code-review-skill
- **claude-api**: LLM app building with Claude SDK
- **architecture-and-design**: system diagrams
- **automation-and-agents**: AI automation and context engineering
- **professional-development**: enterprise-grade workflows
- **productivity-tools**: multi-language enhancements
- **plugin-marketplace**: marketplace integration

When modifying skills, ensure they fit their collection's scope.

## Development Workflow

### Adding a New Skill

1. Create a folder in `skills/` with a kebab-case name
2. Add a `SKILL.md` with required YAML frontmatter and instructions
3. Add supporting files (docs, code examples) as needed
4. Register in `.claude-plugin/marketplace.json` under the appropriate plugin collection

### Validating a Skill

- Ensure `SKILL.md` has valid YAML frontmatter (name + description)
- Description should be clear about when Claude should use the skill (trigger conditions)
- Instructions should be unambiguous and reference external docs/tools when needed
- Test by using `/skill` in Claude Code to verify it activates as expected

### Publishing

The `.claude-plugin/marketplace.json` configuration allows installation via:
```
/plugin install [collection-name]@rickysanch12-skills
```

## Key Conventions

- **Skill Names**: Use kebab-case, lowercase (e.g., `code-review-skill`, not `CodeReviewSkill`)
- **Descriptions**: Write trigger conditions explicitly (e.g., "TRIGGER when: file contains X", "SKIP: if Y is present")
- **Instructions**: Be concise and link to external documentation when appropriate
- **Language**: Match Claude's conventions—use "Claude" not "you", "the user" not "they"
- **No Versioning**: Overwrite skills in place; marketplace always serves the latest version

## Documentation References

- [Agent Skills Specification](https://agentskills.io/specification)
- [Creating Custom Skills](https://support.claude.com/en/articles/12512198-creating-custom-skills)
- [Using Skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude)
- [Skills Guide (API)](https://docs.claude.com/en/api/skills-guide#creating-a-skill)

## Repository Metadata

- **Owner**: Ricky Sanchez (ricky@example.com)
- **Version**: 2.0.0
- **License**: Mixed (Apache 2.0 for open source skills, source-available for document skills)
- **Branch Convention**: Use `claude/add-claude-documentation-fQosk` for documentation updates
