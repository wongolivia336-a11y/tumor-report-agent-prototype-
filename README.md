# Tumor Report Agent Prototype

Clickable Next.js UX prototype for a tumor experiment report agent workspace.

Preview: https://tumor-report-agent-prototype.vercel.app/

This repository is intended for design review, user-flow validation, and engineering discussion with full-stack engineers. It is not production backend code.

## Tech Stack

- Next.js App Router
- React
- TypeScript
- CSS in `app/globals.css`
- `lucide-react` icons

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

## Page Routes

- `/` - report agent workbench prototype

The route entry is intentionally small:

- `app/page.tsx` renders `components/ReportWorkbench.tsx`
- `app/layout.tsx` wires metadata and global styles

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

## Core Components

- `components/ReportWorkbench.tsx`
  Main client-side prototype screen and local demo state orchestration.

- `WorkspaceSidebar`
  Workspace / project / chat navigation model.

- `UploadEmptyState`
  File upload and required-file readiness experience.

- `Conversation`
  Main task flow, activity chains, agent replies, and artifact cards.

- `Composer`
  Bottom input area, upload shortcut, warning confirmation, and review confirmation.

- `WarningDecisionPanel`
  Compressed warning confirmation card with hover/click expansion.

- `ReviewDecisionPanel`
  Compressed expert suggestion confirmation card with hover/click expansion.

- `HoverInspector`
  Right-side hover/pin evidence and artifact panel.

- `ArtifactPreviewModal`
  Preview-only artifact viewer.

## Mock Data Location

- `lib/mock-data.ts`
  Activity chains, warnings, review modules, export items, trace references, and expert profiles.

- `lib/types.ts`
  Business types including `User`, `UploadedFile`, `ReportRun`, `ValidationStep`, `WarningItem`, `ReviewModule`, `ExportItem`, and `ApiResponse`.

- `lib/workflow.ts`
  Workflow status mapping and local prototype helpers.

- `lib/mock-service.ts`
  Prototype-only mock service shaped like the future backend API contract.

## Workflow State Mapping

| UI Stage | Backend-Oriented Status | Meaning |
|---|---|---|
| `empty` | `idle` | No files selected |
| `uploaded` | `uploaded` | Files are present and may be ready |
| `validating` | `validating` | Validation activity chain is running |
| `warning` | `warning_required` | User must accept or reject warning risk |
| `generating` | `generating` | Report and package generation is running |
| `review` | `reviewing` | Expert review modules require confirmation |
| `exported` | `ready_to_export` | Delivery package is ready after review confirmation |

`failed` is defined in `WorkflowStatus` for future backend work, but the approved visual prototype does not currently force a failed state.

## Future API Integration

API contract draft:

- `lib/api-contract.ts`
- `docs/API_CONTRACT.md`

Planned backend operations:

- Create task
- Upload file
- Get task detail
- Get validation result
- Confirm warning
- Get module review status
- Trigger export

## Notes For Engineers

- The prototype prioritizes UX fidelity over production architecture.
- The main interface currently lives in `components/ReportWorkbench.tsx`.
- The visual system and interaction behavior are in `app/globals.css`.
- Only the delivery package is represented as downloadable; Word and intermediate artifacts are preview-only.
- Future engineering handoff should replace local mock state with real APIs after the interaction model is approved.
- See `docs/HANDOFF.md` for detailed engineering guidance.
