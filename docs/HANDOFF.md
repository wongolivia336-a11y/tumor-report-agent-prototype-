# Engineering Handoff

## Purpose

This repository contains a clickable Next.js UX prototype for a tumor experiment report agent workspace.

It is prepared for full-stack engineering review, API planning, and future backend integration. It is not production backend code.

## Documentation Sources

- `README.md`
  Project entry point, preview links, run instructions, and repository map.

- `CHANGELOG.md`
  Version history and important iteration notes.

- `AGENTS.md`
  Project-specific instructions for Codex/agent handoff.

- `docs/DESIGN.md`
  Current design source of truth.

- `docs/API_CONTRACT.md`
  Draft backend API contract.

- `docs/archive/`
  Historical worklogs, UX reviews, presentation drafts, and older change notes.

## Pages / Routes

- `/`
  Main report agent workbench prototype.

The App Router entry is intentionally thin:

- `app/page.tsx` imports and renders `components/ReportWorkbench.tsx`.
- `app/layout.tsx` provides global metadata and stylesheet wiring.

## Key Files

- `components/ReportWorkbench.tsx`
  Main client-side prototype screen. It preserves the approved visual design and local mock state transitions.

- `app/globals.css`
  Approved visual system, layout, spacing, cards, hover states, panels, modals, and responsive rules.

- `docs/DESIGN.md`
  Current design system and interaction rules. Use this before making visual or UX changes.

- `lib/types.ts`
  Core TypeScript business types for users, report runs, uploaded files, warnings, reviews, exports, and API responses.

- `lib/mock-data.ts`
  Centralized mock data for activity chains, warnings, review modules, export items, trace references, and expert profiles.

- `lib/workflow.ts`
  Workflow status mapping and small helpers for mock file classification, file size formatting, and activity-step generation.

- `lib/api-contract.ts`
  Future backend API contract draft.

- `lib/mock-service.ts`
  Prototype-only mock implementation shaped like the future API contract.

## Preserved UX Decisions

- The sidebar models workspace -> project -> chat hierarchy.
- Upload is the task entry point; chat is not treated as the only interaction model.
- The agent process is shown as an activity chain, not as raw chain-of-thought or tool-call logs.
- Warning confirmation is compressed by default and expands on hover or click.
- Users remain responsible for accepting warning risk and confirming expert review items.
- Word report is preview-only and exported through the delivery package.
- Only the delivery package shows a download affordance.
- The right-side inspector is a secondary evidence layer that can be hovered or pinned.

## Workflow States

The UI currently uses `Stage` for display and maps it to backend-oriented `WorkflowStatus`.

| UI Stage | Workflow Status | Meaning |
|---|---|---|
| `empty` | `idle` | No files selected |
| `uploaded` | `uploaded` | Required files may be ready |
| `validating` | `validating` | Validation activity chain running |
| `warning` | `warning_required` | User must accept or reject warning risk |
| `generating` | `generating` | Report and delivery package generation running |
| `review` | `reviewing` | Expert review modules require confirmation |
| `exported` | `ready_to_export` | Review is confirmed and delivery package is ready |

`failed` is defined in `WorkflowStatus` for future backend integration, but the current visual prototype does not force a failed state into the approved design.

## Future API Integration Points

Drafted in `lib/api-contract.ts`:

- `createTask`
- `uploadFile`
- `getTask`
- `getValidationResult`
- `confirmWarning`
- `getReviewModules`
- `triggerExport`

The current UI does not call these APIs yet. Use `lib/mock-service.ts` as the adapter shape when replacing local state with real backend calls.

## Suggested Engineering Next Steps

1. Keep the approved visual layer stable while connecting APIs.
2. Replace local file selection state with `uploadFile`.
3. Replace timer-driven validation/generation progress with backend job status.
4. Map validation results into `WarningItem[]`.
5. Map expert review responses into `ReviewModule[]`.
6. Add real permission checks before package download.
7. Add production-grade failed states after API error shapes are known.
8. Split `ReportWorkbench.tsx` further only after API boundaries are stable.

## Prototype-Only Parts

- Timer-based status transitions.
- Mock file classification by extension.
- Static warning/review/export data.
- Preview modal content.
- Download buttons without real download action.

## Visual Change Policy

This handoff pass should not change layout, color, typography, spacing, rounded corners, shadows, copy, or interaction timing. Treat `app/globals.css` and existing class names as the current approved design surface.
