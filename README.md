# Spec Driven Development

AI-powered development workflow that uses Notion as the Spec hub and GitHub as the code hub.

## Overview

This repository contains a Claude Code skill and templates for implementing a structured, spec-first development process. Every feature starts with a specification document before any code is written.

## Core Principles

1. **Spec First** - Write specifications before code
2. **Single Source of Truth** - Notion for docs, GitHub for code (no duplication)
3. **Traceability** - All code links to specs, all PRs link to issues
4. **AI Transparency** - AI collaboration is logged in AI Sessions
5. **Structural Consistency** - All projects follow the same structure

## Repository Structure

```
spec-driven-dev/
├── SKILL.md                    # Claude Code skill definition
├── assets/
│   └── github-templates/       # GitHub template files
│       ├── CONTRIBUTING.md
│       ├── PULL_REQUEST_TEMPLATE.md
│       └── ISSUE_TEMPLATE/
│           ├── bug.md
│           └── feature.md
└── references/                 # Reference documents & templates
    ├── api-spec-template.md
    ├── db-schema-template.md
    ├── initialization-checklist.md
    ├── notion-schema.md
    └── project-hub-template.md
```

## Workflow

```
New Project → Initialize Notion Hub → Create GitHub Repo → Link Together
     ↓
Feature Request → Write Spec (Notion) → Create Issue (GitHub)
     ↓
Implement → Create PR → Review → Merge → Update Spec Status
```

## Getting Started

### Prerequisites

- Claude Code CLI with Notion MCP configured
- GitHub account

### Project Initialization

1. Create a Notion Project Hub using the [project-hub-template](references/project-hub-template.md)
2. Set up databases: Specs, AI Sessions, Decisions (ADR)
3. Create GitHub repository with templates from [github-templates](assets/github-templates/)
4. Link Notion and GitHub

### Feature Development

1. Write Feature Spec in Notion (status: Draft → Review → Approved)
2. Create GitHub Issue with Spec link
3. Create feature branch: `feature/spec-{id}`
4. Implement and log decisions in AI Sessions
5. Create PR linking to Issue and Spec
6. After merge, update Spec status to Implemented

## Templates

| Template | Purpose |
|----------|---------|
| [API Spec](references/api-spec-template.md) | REST API endpoint documentation |
| [DB Schema](references/db-schema-template.md) | Database table definitions |
| [Project Hub](references/project-hub-template.md) | Notion project home page |
| [Notion Schema](references/notion-schema.md) | Database field definitions |

## Branch Naming

- Feature: `feature/spec-{id}` or `feature/{short-desc}`
- Bugfix: `fix/{issue-number}-{short-desc}`
- Docs: `docs/{short-desc}`

## Commit Message Format

```
<type>(<scope>): <subject>

[body]

Spec: <notion-spec-url>
```

Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`

## License

MIT
