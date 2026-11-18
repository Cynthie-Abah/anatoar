# LLD — Interactive 3D Anatomy Viewer

## Purpose

Provide a reusable viewer for loading and exploring anatomical GLB/GLTF models.

## User stories

- As a learner, I can rotate and zoom the model to understand its shape.
- I can select a visible structure and see its name and explanation.
- I can isolate a structure and restore the full model.
- I can reset the camera and selection.

## Main components

- `AnatomyViewer`: feature-level container.
- `AnatomyCanvas`: React Three Fiber canvas.
- `ModelLoader`: loads and reports model state.
- `ViewerControls`: reset, zoom, and display controls.
- `StructureSelection`: raycast selection and mesh-to-structure mapping.
- `StructureDetails`: selected structure information.
- `ModelStatus`: loading and error UI.

## Data contract

Each model includes:
- stable model ID
- asset path
- asset license and attribution
- mesh-name to structure-ID mapping
- structure metadata and source references

Mesh names are not guaranteed to be stable across arbitrary model revisions. Validate mappings whenever a model asset changes.

## Interaction flow

1. User opens a model.
2. Viewer loads the GLB/GLTF asset.
3. Loading indicator remains visible until the model is ready.
4. User rotates/zooms with pointer or touch controls.
5. User selects a mesh.
6. Raycasting resolves the mesh to a structure ID.
7. UI displays the selected structure.
8. Highlight/isolation is applied.
9. Reset restores visibility/material state and camera defaults.

## Highlighting

- Preserve original material references or clone materials safely before modification.
- Avoid mutating shared materials in a way that unintentionally highlights other meshes.
- Restore original appearance on deselection, reset, and unmount.
- Do not rely on color alone; also show a visible selection label.

## Isolation

- Store original visibility for every affected mesh.
- Hide non-selected mapped meshes only when isolation is activated.
- Restore all original visibility values on reset or unmount.
- Define expected behavior for selecting a child mesh or a group.

## Error handling

Handle:
- missing asset
- invalid GLB/GLTF
- failed network/static asset load
- missing mesh mapping
- unsupported WebGL or context loss
- model too large for device memory

Provide a readable error and a way to return to the lesson.

## Performance and cleanup

- Lazy-load model assets.
- Optimize mesh and texture sizes before committing.
- Use suspense/loading boundaries appropriately.
- Dispose resources when no longer used.
- Avoid state updates per rendered frame.
- Test touch controls on physical mobile hardware.

## Acceptance criteria

- Model loads with visible progress/loading feedback.
- Orbit, zoom, and reset work with mouse and touch.
- Mapped structures can be selected.
- Highlight and isolation can be reset.
- Missing mappings do not crash the viewer.
- Unmounting the viewer does not leave animation loops or listeners running.
