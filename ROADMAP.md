# AnatoAR Roadmap

This roadmap describes planned work, not completed features. Update checkboxes only when the corresponding work has actually been implemented and tested.

## Phase 0 — Repository and project foundation

- [ ] Create React + TypeScript + Vite application.
- [ ] Add formatting, linting, and type-check scripts.
- [ ] Establish feature-oriented folder structure.
- [ ] Add basic responsive application shell and navigation.
- [ ] Add project documentation and accepted open-source license.
- [ ] Add a documented process for tracking 3D asset licenses and sources.

## Phase 1 — 3D anatomy foundation

- [ ] Select and review a licensed heart model.
- [ ] Record model source, creator, license, attribution, and modifications.
- [ ] Load GLB/GLTF models in the browser.
- [ ] Implement orbit, zoom, and reset camera controls.
- [ ] Define a stable mapping between model meshes and anatomy structure IDs.
- [ ] Implement structure selection and highlighting.
- [ ] Implement isolate and restore actions.
- [ ] Add structure names and concise educational descriptions.
- [ ] Add loading, error, and unsupported-model states.

## Phase 2 — Guided anatomy learning

- [ ] Create the cardiovascular learning overview.
- [ ] Add structured heart anatomy content.
- [ ] Add guided learning steps linked to model structures.
- [ ] Add a small set of reviewed knowledge-check questions.
- [ ] Add quiz feedback and score calculation on the client.
- [ ] Add bookmarks and local-only progress.
- [ ] Make all core learning content usable without AR.

## Phase 3 — Anatomy animations

- [ ] Support animation clips included in GLB assets.
- [ ] Add play, pause, restart, and animation selection controls.
- [ ] Link animation stages to explanatory text.
- [ ] Verify animation performance on mobile devices.
- [ ] Provide a non-animated explanation where animation is unavailable.

## Phase 4 — Image-tracked AR

- [ ] Add a user-facing explanation before camera permission is requested.
- [ ] Integrate MindAR behind an AR adapter.
- [ ] Prepare and document a licensed image target.
- [ ] Display the selected anatomy model when the target is detected.
- [ ] Handle target found/lost states.
- [ ] Add clear stop-camera and exit controls.
- [ ] Verify camera tracks and event listeners are cleaned up on exit.

## Phase 5 — WebXR AR

- [ ] Detect immersive AR and hit-test support at runtime.
- [ ] Provide a clear unsupported-device fallback.
- [ ] Request an AR session only after an explicit user action.
- [ ] Implement reticle and surface placement on supported devices.
- [ ] Support model repositioning, rotation, and scale within safe bounds.
- [ ] Handle session end, permission denial, and interrupted sessions.
- [ ] Test on physical compatible devices.

## Phase 6 — Quality and release preparation

- [ ] Add unit and component tests for core interactions.
- [ ] Add end-to-end tests for browsing, viewing, learning, and quizzes.
- [ ] Test desktop and mobile layouts.
- [ ] Test AR capability and failure states on real devices.
- [ ] Optimize model size and loading performance.
- [ ] Audit dependencies, secrets, asset licenses, and privacy behavior.
- [ ] Deploy over HTTPS.
- [ ] Add screenshots and a short demonstration to the README.

## Explicitly outside the BYOP scope

- AI anatomy assistant, AI inference, or AI-generated learning content.
- AI model training, fine-tuning, evaluation, or benchmarking.
- User accounts, authentication, server-side learner profiles, or cloud progress.
- Collection or processing of personal, medical, patient, or other regulated data.
- Clinical diagnosis, treatment recommendations, or clinical decision support.
- Patient-specific anatomy reconstruction or medical imaging workflows.
- Surgical planning or clinical procedure simulation.
- Real-time multi-user AR.
- Native iOS or Android applications.
- A custom 3D modelling or content-authoring suite.
