# Tumor Report Agent Prototype

Clickable Next.js prototype for a tumor experiment report agent workspace.

This repository is for design review, user-flow validation, and engineering handoff. It is not production backend code.

## Preview

- Local dev server: http://localhost:4196
- Vercel preview: https://tumor-report-agent-prototype.vercel.app/
- GitHub remote: https://github.com/wongolivia336-a11y/tumor-report-agent-prototype-.git

## Quick Start

```bash
npm install
npm run dev -- --port 4196
```

Open:

```text
http://localhost:4196
```

## Documentation Map

- [CHANGELOG.md](CHANGELOG.md)
  Version history and important iteration notes.

- [AGENTS.md](AGENTS.md)
  Project-specific rules for Codex/agent handoff.

- [docs/DESIGN.md](docs/DESIGN.md)
  Current design system and interaction rules.

- [docs/HANDOFF.md](docs/HANDOFF.md)
  Engineering handoff notes for future API integration.

- [docs/API_CONTRACT.md](docs/API_CONTRACT.md)
  Draft backend API contract.

- [docs/SKILLS_INVENTORY.md](docs/SKILLS_INVENTORY.md)
  Current local skills inventory and cleanup notes.

- [docs/archive/](docs/archive/)
  Historical worklogs, UX reviews, change notes, and presentation drafts. These are kept for traceability but are not the active source of truth.

## Repository Map

- `app/`
  Next.js App Router entry files. `app/page.tsx` renders the prototype screen and `app/globals.css` contains the visual system.

- `components/`
  React UI components. The main workbench prototype currently lives in `components/ReportWorkbench.tsx`.

- `lib/`
  Mock data, workflow helpers, type definitions, and API contract shape.

- `docs/`
  Active design, handoff, API, skills, and archive documentation.

- `public/`
  Static assets such as the BioAZ logo.

- `output/`
  Local generated verification artifacts. This is not source code and should not be committed.

## Tech Stack

- Next.js App Router
- React
- TypeScript
- CSS in `app/globals.css`
- `lucide-react` icons

## Prototype Scope

- Mock data only
- No backend APIs
- No database
- No authentication
- No real file parsing
- No real report generation
- No real download or permission service

## Main Flow

```text
Upload DOCX / XLSX files
-> Validation activity chain
-> Warning confirmation
-> Report generation
-> Expert review
-> Artifact preview
-> Delivery package handoff
```

## Key Implementation Notes

- The route entry is intentionally small: `app/page.tsx` renders `components/ReportWorkbench.tsx`.
- The main prototype state is local and mock-driven.
- The right-side inspector is a secondary evidence and artifact layer.
- Warning and expert suggestion previews use the same modal system as artifact previews where possible.
- Future backend integration should replace mock state after the interaction model is approved.

## Validation

Run the main check before committing:

```bash
npm run typecheck
```
