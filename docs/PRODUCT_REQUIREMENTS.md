# AnatoAR — Product Requirements Document

**Status:** Initial project specification  
**Product type:** Browser-based 3D and augmented reality anatomy learning platform  
**Initial content focus:** Cardiovascular system / heart

## 1. Product overview

AnatoAR helps nursing and other health-science students explore anatomy using interactive 3D models, guided explanations, animations, and optional augmented reality experiences.

The initial release will focus on a high-quality heart learning experience rather than attempting to cover the entire human body at once.

## 2. Problem

Anatomy learners often rely on static diagrams, textbooks, and two-dimensional illustrations. These resources are valuable but can make it difficult to understand spatial relationships, orientation, and how structures relate to one another.

AnatoAR aims to make selected anatomy topics more explorable through direct interaction with 3D models and guided learning content.

## 3. Target users

- Nursing students.
- Medical and allied-health students.
- Other learners studying foundational human anatomy.

The product is an educational aid, not a clinical tool.

## 4. Product goals

- Let learners explore a selected anatomical model in 3D.
- Connect visible model structures to concise educational explanations.
- Demonstrate selected anatomical concepts through animation.
- Offer AR as an optional enhancement on compatible devices.
- Provide short knowledge checks.
- Allow bookmarks and basic progress to remain locally on the learner's device.
- Work on desktop and mobile browsers, with graceful fallback where features are unsupported.

## 5. Non-goals

The BYOP version will not provide:
- AI assistants or any AI inference.
- User accounts or cloud-synced profiles/progress.
- Collection or processing of personal, patient, medical, or regulated data.
- Diagnosis, treatment recommendations, or clinical decision support.
- Patient-specific 3D reconstruction.
- Surgical planning or clinical procedure simulation.
- Native mobile apps.
- Real-time multi-user AR.
- A general-purpose 3D authoring tool.

## 6. MVP features and requirements

### 6.1 Application shell and anatomy library

- The user can open the application without creating an account.
- The user can browse the available anatomy topic(s).
- Each topic displays a title, short overview, and available learning activities.
- The initial release includes a cardiovascular topic and heart model.

### 6.2 3D anatomy viewer

- Load an optimized GLB/GLTF model.
- Rotate, zoom, and reset the camera.
- Select a mapped anatomical structure.
- Highlight the selected structure.
- Display the structure name and reviewed description.
- Isolate a structure and restore the complete model.
- Show loading and error states.
- Provide usable touch and mouse controls.

### 6.3 Guided learning

- Present learning content in short, structured sections.
- Allow a learning step to select or highlight a related model structure.
- Clearly distinguish explanatory content from interactive controls.
- Provide a useful reading experience without requiring AR.

### 6.4 Animations

- Play, pause, and restart available model animations.
- Display a short explanation for the current animation or stage.
- Provide a static explanation if the animation cannot load.

### 6.5 Image-tracked AR

- Explain why camera access is needed before requesting permission.
- Start image tracking only after an explicit user action.
- Display a model when a supported target image is detected.
- Communicate target-found and target-lost states.
- Allow the user to exit and stop the camera.
- Do not upload or store camera frames.

### 6.6 WebXR AR

- Detect support at runtime.
- Start immersive AR only after an explicit user action.
- Show a placement reticle where hit testing is supported.
- Place and manipulate the anatomy model.
- End the session cleanly.
- Show a fallback message and link to the standard 3D viewer if unsupported.

### 6.7 Assessments

- Provide short multiple-choice or true/false knowledge checks.
- Show feedback after an answer is submitted.
- Calculate results locally.
- Do not transmit quiz answers or scores to a server.

### 6.8 Bookmarks and progress

- Let a learner bookmark selected structures or lessons.
- Store simple completion state locally in the browser.
- Provide a way to clear locally stored application data.
- Do not associate stored data with an identity or transmit it.

## 7. UX and accessibility requirements

- Responsive layouts for desktop and mobile.
- Clear labels for viewer and AR controls.
- Keyboard-accessible navigation and controls where applicable.
- Visible focus states.
- Text contrast suitable for reading.
- Do not communicate selected state by color alone.
- Provide loading, empty, error, permission-denied, and unsupported-device states.
- Avoid making AR necessary to complete a lesson.

## 8. Performance requirements

- Load 3D assets only when needed.
- Use appropriately optimized models and textures.
- Avoid unnecessarily high polygon counts and texture resolutions.
- Provide loading feedback for large assets.
- Dispose of Three.js resources when no longer needed.
- Test on representative mid-range mobile devices.
- Keep the standard learning content usable on devices that cannot run AR.

## 9. Content quality and asset requirements

- Anatomy descriptions must be reviewed against reputable educational references.
- Record references and review status for educational content.
- Record source, author/creator, license, attribution requirements, and modifications for each external model, image, texture, and target.
- Do not assume that an asset found online is free to reuse.
- Do not publish assets whose license is unknown or incompatible with the intended use.

## 10. Privacy and data requirements

- No account creation or authentication.
- No backend database of learner information.
- No personal, patient, or regulated data.
- No analytics or tracking in the BYOP scope.
- Local progress and bookmarks remain on the user's device.
- Camera access is optional, user-initiated, and used only for the AR session.
- Camera tracks and AR resources are stopped and released on exit.

## 11. MVP acceptance criteria

The MVP is acceptable when:
1. The application runs locally and has documented setup steps.
2. A learner can open the cardiovascular topic without signing in.
3. The heart model loads and can be rotated, zoomed, and reset.
4. At least the documented mapped structures can be selected and identified.
5. Selection highlighting and isolation can be reset reliably.
6. At least one guided learning path connects explanations to model structures.
7. At least one reviewed knowledge check works entirely client-side.
8. AR capability is detected at runtime and unsupported devices receive a clear fallback.
9. Implemented AR experiences can be exited without leaving camera tracks running.
10. No prohibited AI inference or personal-data processing is present.
11. Asset provenance and licenses are documented.
12. Tests and known limitations are documented.

## 12. Success indicators

For the initial project, success is measured by working product behavior rather than collecting user data:
- Core 3D interactions work reliably.
- Learners can complete the heart learning path.
- AR fallback behavior is clear.
- The experience remains responsive on supported mobile devices.
- The repository has reproducible setup, tests, documentation, and a visible roadmap.
