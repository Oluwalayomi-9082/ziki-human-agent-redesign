# Ziki Human Agent Interaction

An unofficial, outcome-focused redesign prototype of Ziki, built with React, TypeScript, and Vite. This is an independent submission, not the official Ziki application.

## Experience

- Product: Overview and delivered outcomes, with search, filters, details, and JSON export.
- Notifications: decisions that need human attention.
- Agents: listed agents, their functions, and buttons to view their outcomes.
- Profile: System, Light, and Dark modes, saved on the device.

All records are sample data. Decisions update browser memory only and reset on reload. No live agents, credentials, repositories, or Ziki APIs are connected.

## Local development

```sh
npm install
npm run dev
```

## Production build

```sh
npm run build
npm run preview
```

The build runs TypeScript validation and writes the static site to dist/.

## Deploy to Vercel

Import this GitHub repository into Vercel. Use the Vite preset, npm run build as the build command, and dist as the output directory. No environment variables are required. Configuration is included in vercel.json.

## Product reference

Original product: https://ziki.dev/
Product context: https://ziki.dev/llms.txt

## Submission proposal

See [the submission package](submission/README.md) for the case study, before-and-after screenshots, reviewer walkthrough, and developer handoff.

## Consolidated submission

Live demo: https://ziki-human-agent-redesign.vercel.app/

The original redesign now includes the whimsical interactions: pointer-following Overview eyes with gentle blinking, a settling notification bell, agent acknowledgement, animated approval feedback, and all-clear sparkles. Reduced-motion preferences disable animated tracking and motion.

Ready-to-merge outcomes expose Approve merge directly in an Action column between Agent and Delivered. Result details remain a separate button. All approval actions remain demonstrations using local state.

The notification bell gently settles again every five minutes while decisions remain pending in the open page. The timer is cleared when there are no pending decisions. Reduced-motion preferences suppress the wiggle. Browsers may throttle reminders in inactive tabs.
