# Tumor Report Agent Prototype

Clickable Next.js UX prototype for a tumor experiment report agent workspace.

Preview: https://tumor-report-agent-prototype.vercel.app/

This repository is intended for design review, user-flow validation, and engineering discussion with full-stack engineers. It is not production backend code.

## Run Locally

```bash
npm install
npm run dev
```

Open:

```text
http://localhost:3000
```

Or run on a custom port:

```bash
npm run dev -- --port 4196
```

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

## Notes For Engineers

- The prototype prioritizes UX fidelity over production architecture.
- The main interface currently lives in `app/page.tsx`.
- The visual system and interaction behavior are in `app/globals.css`.
- Only the delivery package is represented as downloadable; Word and intermediate artifacts are preview-only.
- Future engineering handoff should extract mock data, split components, and connect real APIs after the interaction model is approved.
