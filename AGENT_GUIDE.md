# Coding Agent Guide — AnatoAR

This file defines the implementation boundaries for coding assistants working in this repository.

## Product goal

Build a browser-based anatomy learning platform. The first complete learning experience focuses on the cardiovascular system and an interactive 3D heart.

## Non-negotiable BYOP boundaries

Do not implement or introduce:

- AI inference, AI assistants, LLM API calls, model serving, training, fine-tuning, evaluation, or benchmarking.
- User registration, login, authentication, user profiles, or server-side accounts.
- Backend storage or transmission of learner identities, quiz history, bookmarks, or learning progress.
- Patient data, medical records, diagnostic information, or regulated personal data.
- Analytics, telemetry, session replay, tracking pixels, or unnecessary third-party data collection.
- Clinical decision support, diagnosis, treatment recommendations, or patient-specific workflows.

If a requested feature appears to conflict with these boundaries, stop and explain the conflict before implementing it.

## Implementation rules

1. Inspect the existing repository and current conventions before editing.
2. Do not replace working code or restructure the project without a clear reason.
3. Implement one feature at a time in small, reviewable changes.
4. Use TypeScript types for domain entities and component contracts.
5. Keep anatomy metadata and learning content separate from rendering components.
6. Keep Three.js objects, animation mixers, renderers, observers, and camera tracks correctly cleaned up.
7. Do not update React state on every animation frame.
8. Use runtime feature detection for AR; do not rely only on user-agent strings.
9. Keep the standard 3D viewer usable when AR is unavailable.
10. Request camera access only after a user explicitly starts an AR experience.
11. Do not upload camera frames. Stop media tracks when the AR experience ends.
12. Do not invent anatomical facts. Use supplied/reviewed content and clearly flag missing references.
13. Do not add a 3D model, texture, image target, font, or other asset without recording its source and license.
14. Do not add dependencies without explaining why they are needed.
15. Add or update tests for meaningful behavior changes.
16. Run linting, type checking, tests, and production build where available; report commands and results accurately.
17. Never claim a feature is complete if it has not been implemented and tested.

## Preferred technical direction

- React + TypeScript + Vite
- Three.js + React Three Fiber + Drei
- MindAR behind an image-tracking adapter
- WebXR behind a separate immersive-AR adapter
- Zustand for transient client-side state
- Local storage only for non-identifying local preferences/progress
- Vitest, React Testing Library, and Playwright

Do not add a backend or database for the BYOP version unless the project owner first verifies that the proposed data flow remains eligible.

## Expected workflow for each task

Before coding:
- Restate the task and acceptance criteria.
- Inspect relevant files.
- Identify likely risks and affected components.
- Propose the smallest implementation plan.

While coding:
- Follow existing patterns.
- Keep changes scoped.
- Handle loading, empty, error, and unsupported states.
- Keep accessibility and keyboard behavior in mind.

After coding:
- Summarize files changed.
- Explain implementation decisions.
- List tests and commands run, including failures.
- Identify manual checks still required.
- Confirm that no prohibited AI or personal-data functionality was introduced.

## Definition of done

A task is done only when its acceptance criteria are met, relevant tests pass, type/lint/build checks have been run where available, and remaining limitations are stated.
