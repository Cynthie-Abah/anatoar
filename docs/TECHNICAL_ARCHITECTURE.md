# AnatoAR — Technical Architecture

## 1. Architecture summary

AnatoAR is a client-side web application. The BYOP version does not require a backend, account system, or database.

```text
Browser
├── React application
│   ├── Anatomy library and learning UI
│   ├── 3D viewer (React Three Fiber / Three.js)
│   ├── Animation controls
│   ├── AR user interface
│   ├── Assessments
│   └── Local bookmarks and progress
├── Static content
│   ├── Anatomy metadata
│   ├── Learning modules
│   └── Quiz questions
├── Static assets
│   ├── GLB / GLTF models
│   ├── Textures
│   └── Image-tracking targets
└── Browser capabilities
    ├── WebGL
    ├── Camera APIs (image tracking)
    └── WebXR (where supported)
```

## 2. Technology choices

| Area | Preferred technology | Responsibility |
|---|---|---|
| Application | React + TypeScript + Vite | UI and build |
| 3D rendering | Three.js + React Three Fiber | Scene and model rendering |
| 3D helpers | Drei | Camera, controls, loaders, helpers |
| Image tracking | MindAR | Target-based AR |
| Immersive AR | WebXR | AR session and hit testing where supported |
| UI state | Zustand | Transient client-side state |
| Local persistence | Browser localStorage | Non-identifying bookmarks/progress |
| Unit/component tests | Vitest + Testing Library | Core logic and UI |
| E2E tests | Playwright | Browser workflows |

Dependencies should be added only when needed and recorded in the package manifest.

## 3. Application layers

### Presentation layer

React pages and components display the anatomy library, viewer controls, learning content, quizzes, and AR status.

### Feature layer

Feature modules own their user-facing behavior:
- `anatomy-library`
- `anatomy-viewer`
- `animations`
- `ar`
- `learning`
- `assessments`
- `bookmarks`

### Domain/content layer

Plain TypeScript types and static data describe anatomy structures, models, learning modules, and questions. This layer should not depend on React or Three.js.

### Rendering layer

Three.js and React Three Fiber own scene creation, model loading, raycasting, camera controls, animation mixers, and resource disposal.

### Device integration layer

Separate adapters isolate browser APIs:
- image-tracking adapter
- WebXR adapter
- capability detection

The rest of the application should not need to know the implementation details of a specific AR library.

## 4. Suggested source layout

```text
src/
  app/
    routes/
    providers/
  components/
    ui/
  features/
    anatomy-library/
    anatomy-viewer/
    animations/
    ar/
    learning/
    assessments/
    bookmarks/
  data/
    anatomy/
    learning/
    quizzes/
  domain/
    anatomy/
    learning/
  hooks/
  lib/
  state/
  three/
    loaders/
    materials/
    interactions/
  ar/
    capability/
    image-tracking/
    webxr/
  styles/
  test/
public/
  models/
  textures/
  targets/
```

Do not create every directory in advance if it has no code yet. Let the structure grow with implemented features.

## 5. Core domain types

Illustrative TypeScript contracts:

```ts
export type AnatomyStructure = {
  id: string;
  name: string;
  systemId: string;
  description: string;
  meshNames: string[];
  sourceReferences: string[];
  reviewStatus: "draft" | "reviewed";
};

export type AnatomyModel = {
  id: string;
  title: string;
  assetPath: string;
  format: "glb" | "gltf";
  structures: AnatomyStructure[];
  assetLicense: string;
  assetAttribution: string;
};

export type LearningStep = {
  id: string;
  title: string;
  body: string;
  relatedStructureIds: string[];
};

export type QuizQuestion = {
  id: string;
  prompt: string;
  options: { id: string; text: string }[];
  correctOptionId: string;
  explanation: string;
};
```

Keep answer keys in local static content for this no-backend educational MVP. Do not describe client-side quiz answers as secure against inspection.

## 6. State management

Use local component state for isolated UI state and Zustand only for state shared across features, such as:
- selected anatomy structure ID
- active learning step ID
- active animation ID
- AR mode/status
- viewer preferences

Persist only minimal, non-identifying preferences and progress in local storage. Validate and version stored data. Provide a clear-data action. Do not persist camera data, device identifiers, or sensitive information.

## 7. 3D lifecycle

- Load models on demand.
- Keep model loading state explicit.
- Map mesh names to stable anatomy structure IDs through metadata.
- Preserve original material properties before applying selection effects.
- Restore original materials on deselection/reset.
- Dispose geometries, materials, textures, animation mixers, and renderer-owned resources when appropriate.
- Avoid creating duplicate render loops.
- Avoid React state updates on every frame.

## 8. AR capability and fallback

Detect capabilities at runtime. Browser support varies and successful API detection does not guarantee a session will start.

The user journey should be:
1. Open anatomy lesson.
2. Explore the standard 3D viewer.
3. Choose an AR mode.
4. See device/browser support information.
5. Grant camera or AR permission if requested.
6. Interact with the model.
7. Exit AR and release resources.

If AR is unsupported, denied, or fails, keep the standard 3D experience available.

## 9. Deployment

- Deploy the static web application to a suitable static hosting provider.
- Serve production over HTTPS.
- Do not include private keys or server credentials in frontend code.
- Keep `.env` files out of Git.
- Use `.env.example` only if public configuration variables are actually needed.
- Test the production build and AR behavior on physical devices.

## 10. Architecture decisions

- **No backend for BYOP MVP:** avoids unnecessary collection and processing of learner data.
- **No authentication:** learning can begin immediately.
- **Local-only progress:** provides basic continuity without a server-side user record.
- **AR adapters:** isolate experimental and browser-specific APIs.
- **3D-first fallback:** the educational product remains useful without AR.
- **Static reviewed content:** keeps learning content auditable and avoids AI-generated medical claims.
