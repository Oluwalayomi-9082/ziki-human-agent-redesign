# Developer handoff

## Source and build
Repository: https://github.com/Oluwalayomi-9082/ziki-human-agent-redesign
Stack: React 19, TypeScript 5, Vite 6, local SVG icons.

Run npm install, then npm run dev. Run npm run build for TypeScript validation and the production bundle; npm run preview serves that bundle. Vercel configuration is in vercel.json: Vite preset, npm run build, dist output, no environment variables.

## File map
- src/main.tsx: application state, demonstration records, view switching, decisions, result detail dialogs, export, and theme state.
- src/style.css: responsive styles, Ziki branding, and dark theme overrides.
- src/icons.tsx: local SVG icon components.
- index.html: app shell.

## Current behavior
Product shows delivered outcomes; the bell opens human decisions; Agents shows the directory. View outcomes sets an agent search and returns to Product. Filters use local status fields. Approvals only update React state. The profile theme is saved under ziki-theme in localStorage; System listens for OS changes. Views are state-based and do not have separate URLs.

## Integrating real Ziki data
The API reference is https://ziki.dev/llms.txt. Verify its current contracts and the human user's authentication and authorization model before integrating. Agent-key routes are not evidence of an owner-facing browser authentication contract.

1. Add an authenticated backend adapter for owner-facing requests. Keep agent keys out of browser code, localStorage, source control, and exported reports.
2. Replace the local agent and result records with project-scoped server data. Normalize issue state, agent identity, verified result summary, timestamps, and actual reviewer evidence. Never infer completion from text alone.
3. Map pending decisions to supported escalation/question/redesign records. Confirm which endpoint supports each decision type and which user may resolve it. The present cards do not have backend decision IDs.
4. Make approval and merge operations explicit, authorized server mutations with pending, success, failure, and retry states. A successful button click must not imply a completed merge or deployment until the server verifies it.
5. Add loading, authentication-expired, permission-denied, empty, and network-error states. Use stable IDs, server timestamps, idempotency where supported, and concurrency checks so stale decisions cannot be submitted twice.
6. Connect the documented event stream or polling flow through a suitable authenticated channel. Refresh pending counts and outcomes from confirmed server events.
7. Add deep links and routing for shared views; preserve filters in the URL. Split the monolithic app into view, dialog, theme, and data modules as the integration grows.

Suggested view model: Outcome { id, issueId, title, summary, agentId, deliveredAt, status, verificationEvidence }; Decision { id, issueId, type, summary, recommendation, allowedActions, version }; Agent { id, name, role, model, function, connectivityStatus }. These are proposed adapter models, not existing Ziki API schemas.

## Before production
- Obtain approved API access and define the human decision authorization policy.
- Confirm independent-review evidence rather than using demonstration labels.
- Test keyboard navigation, dialog focus containment/restoration, screen-reader announcements, contrast, touch layouts, and reduced-motion preferences.
- Decide durable decision history, user identity, routing, and error recovery.
- Add a lockfile and CI build from a clean install for reproducibility.
- Remove or implement Marketing/Security placeholders and review fictional profile/points before a real rollout.

## Verification
TypeScript and Vite production builds passed during development. The owner reported successful manual feature testing. This is a submission prototype, not a production integration.

## Consolidated interaction update

This submission now includes the whimsical interaction effects in the original application. Overview eyes follow pointer movement and blink; the bell settles; agent avatars acknowledge hover and keyboard focus; approvals animate a checkmark; clearing decisions shows sparkles. Reduced-motion preferences disable motion. Ready-to-merge outcomes include an Approve merge button directly under Action, between Agent and Delivered, without requiring a detail dialog. This changes demonstration state only.
