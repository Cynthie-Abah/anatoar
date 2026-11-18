# LLD — Augmented Reality Experience

## Purpose

Allow learners to view an anatomy model in an AR context on supported devices while preserving the standard 3D viewer as the universal fallback.

## Modes

### Image-tracked AR

Use MindAR to detect a documented target image and render the selected model relative to that target.

### WebXR immersive AR

Use WebXR where the browser/device supports the required immersive AR session and hit-test features. Support is device- and browser-dependent.

## Architecture

Keep AR implementations behind an adapter interface so UI components do not depend directly on a particular library.

Illustrative contract:

```ts
export type ARCapability = {
  supported: boolean;
  reason?: string;
};

export interface ARAdapter {
  checkSupport(): Promise<ARCapability>;
  start(): Promise<void>;
  stop(): Promise<void>;
}
```

The actual interface may need mode-specific methods and typed events during implementation.

## User flow

1. User chooses an AR mode.
2. App explains camera/AR permission requirements.
3. App checks support at runtime.
4. User explicitly starts the experience.
5. Browser permission/session is requested.
6. Model appears when the target is found or a valid placement pose is available.
7. User interacts with the model.
8. User exits.
9. Session, camera tracks, event listeners, and temporary resources are released.

## Image tracking behavior

- Register the target image and associated model.
- Display a waiting state before target detection.
- On target-found, show the model.
- On target-lost, hide or pause the model and show a clear status.
- Avoid rapidly toggling visibility if tracking briefly fluctuates.
- Provide instructions for printing or displaying the target at a suitable size.
- Record target image provenance and license.

## WebXR behavior

- Check `navigator.xr` and relevant session support at runtime.
- Request immersive AR only after a user action.
- Request hit-test support only when needed and supported.
- Use a reticle to indicate a valid placement pose.
- Place the model using the hit-test pose.
- Provide bounded scale and rotation controls.
- Handle session end and visibility changes.
- Do not assume that API availability guarantees a successful AR session.

## Permission and privacy

- Do not request camera permission on initial page load.
- Explain why camera access is needed.
- Do not upload, save, or transmit camera frames.
- Stop all media tracks on exit.
- Remove event listeners and dispose temporary resources.
- Provide a non-AR alternative if permission is denied.

## Fallback states

- AR not supported: offer standard 3D viewer.
- Permission denied: explain how to continue without AR.
- Target not found: show positioning instructions.
- Session interrupted: return to standard viewer with an explanation.
- Asset load failure: show a recoverable error.

## Testing

Test on actual devices. Desktop emulation alone is not sufficient for validating camera tracking or immersive AR.

## Acceptance criteria

- Capability is checked at runtime.
- Unsupported devices can still complete the lesson in 3D.
- AR starts only after explicit user action.
- Permission denial is handled without breaking the app.
- Exiting AR releases camera/session resources.
- No camera frames are uploaded or stored.
