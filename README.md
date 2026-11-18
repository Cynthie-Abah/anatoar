# AnatoAR

AnatoAR is an interactive anatomy learning platform that helps nursing and other health-science students explore human anatomy through 3D models, animations, and augmented reality (AR).

The project is being developed as an independent, browser-based learning tool. Its initial focus is the cardiovascular system, beginning with an interactive 3D heart.

## Project status

**Stage:** Planning / early development  
**Initial learning area:** Cardiovascular system  
**Primary experience:** Desktop and mobile web browsers

Features are being developed incrementally. The roadmap describes planned work; it should not be read as a claim that every feature is already implemented.

## Planned features

- Browse structured anatomy learning content.
- Load and explore 3D anatomical models.
- Rotate, zoom, select, highlight, isolate, and reset anatomical structures.
- View guided animations that explain selected anatomical concepts.
- Launch image-tracked AR where supported.
- Launch WebXR immersive AR on compatible devices and browsers.
- Complete knowledge-check quizzes.
- Save bookmarks and basic learning progress locally in the browser.

## Technology direction

- React, TypeScript, and Vite
- Three.js, React Three Fiber, and Drei
- MindAR for image-tracked AR
- WebXR for supported immersive AR experiences
- Zustand for client-side application state
- Browser local storage for local-only preferences and progress
- Vitest and React Testing Library for unit/component tests
- Playwright for browser-level tests

The exact dependencies and versions will be recorded in `package.json` as implementation begins.

## Privacy and data scope

The BYOP project scope is deliberately designed not to collect or transmit learner personal data.

- No user accounts or authentication in the BYOP scope.
- No server-side learner profiles or progress records.
- Bookmarks and progress, if implemented, remain in the user's browser.
- Camera access is requested only when the user starts an AR feature.
- Camera frames are processed for the AR experience and are not uploaded by the application.
- Do not add analytics, telemetry, tracking pixels, or third-party data collection without first reviewing the project scope and BYOP eligibility.

Anatomical content is educational. AnatoAR is not a diagnostic, treatment, or clinical decision-support tool.

## Getting started

The project is under active development. Once the application scaffold and package scripts are in place:

```bash
npm install
npm run dev
```

Use the scripts defined in `package.json`; the commands above are the intended default setup.

For AR testing, use a supported device/browser and a secure context (HTTPS, or localhost during local development). AR capability varies by browser and device. The standard 3D viewer should remain available when AR is unsupported or permission is denied.

## Repository structure

The structure may evolve as implementation proceeds. The intended organization is feature-oriented:

```text
src/
  app/
  components/
  features/
    anatomy-library/
    anatomy-viewer/
    animations/
    ar/
    learning/
    assessments/
    bookmarks/
  data/
  hooks/
  lib/
  state/
  styles/
  three/
public/
  models/
  targets/
  textures/
docs/
  lld/
```

## Documentation

- [Product requirements](docs/PRODUCT_REQUIREMENTS.md)
- [Technical architecture](docs/TECHNICAL_ARCHITECTURE.md)
- [Roadmap](ROADMAP.md)
- [Agent implementation guide](AGENT_GUIDE.md)
- [3D viewer LLD](docs/lld/3D_VIEWER.md)
- [AR experience LLD](docs/lld/AR_EXPERIENCE.md)
- [Learning and assessment LLD](docs/lld/LEARNING_AND_ASSESSMENTS.md)
- [Privacy, security, and asset policy](docs/PRIVACY_SECURITY_AND_ASSETS.md)

## Development principles

1. Build a useful standard 3D experience before adding AR complexity.
2. Treat AR as progressive enhancement, not as a requirement for using the app.
3. Keep anatomical structure metadata separate from rendering code.
4. Use licensed assets and record their provenance.
5. Keep the application usable on mid-range mobile devices.
6. Do not claim anatomical accuracy beyond what has been reviewed.
7. Keep the BYOP scope free of AI inference and personal-data processing.

## Educational disclaimer

AnatoAR is an educational visualization tool. It is not a substitute for formal teaching, approved anatomy references, clinical supervision, or professional medical advice. Content and models must be reviewed against reputable anatomy references before being presented as authoritative.

## License

The repository should use an accepted open-source license selected by the project owner. If MIT is selected, add the complete MIT License text in a root-level `LICENSE` file before submitting to BYOP. Do not submit with a missing or mismatched license.
