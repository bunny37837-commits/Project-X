# PLANS.md — SatTrack Pro Roadmap

## Status
- Current Milestone: V3
- State: In Progress

## V1 — Core working feature
### Goal
Deliver a runnable single-file SatTrack Pro application with a tactical UI shell, Cesium globe, and live telemetry.

### Done Means
- `index.html` renders full-screen tactical layout with top bar, left sidebar, right detail panel, and bottom HUD.
- Cesium globe initializes with required viewer options and Esri World Imagery base layer.
- TLE, ISS, and Aircraft integrations are wired with update intervals.
- Satellite rendering, category assignment, selection, and search/filter controls function.

### Tasks
- [x] Implement fixed layout and design system tokens in a single HTML file.
- [x] Initialize Cesium with required operational settings.
- [x] Integrate live sources (TLE + ISS + aircraft) and render entities.
- [x] Add category filtering, mission feed list, and detail panel selection.

## V2 — Complete feature set
### Goal
Complete all requested interaction and monitoring systems.

### Done Means
- Visual modes (NORMAL/NIGHT/THERMAL/CRT) are fully functional.
- Toast notification system replaces browser alerts for runtime events.
- Keyboard shortcuts and control actions are available.
- Orbit trails, coordinate HUD updates, and fullscreen/pause controls work.

### Tasks
- [x] Implement mode switch controls and CSS visual pipelines.
- [x] Add toast system with typed severity styling.
- [x] Implement keyboard shortcuts and right-panel open/close flows.
- [x] Add coordinate tracking and FPS monitoring in HUD/stats.

## V3 — Production ready
### Goal
Ship hardened production build with caching, runtime resilience, and documentation sync.

### Done Means
- Satellite count capped at 600 and entity dedup/update strategy enforced.
- TLE localStorage cache uses 1-hour TTL.
- Loading screen and WebGL fallback behavior present.
- Documentation updated for milestones and project status.
- Build/test checks pass and runnable output exists.

### Tasks
- [x] Enforce render/update performance constraints and periodic refresh loops.
- [x] Add loading state and WebGL-required fallback panel.
- [x] Complete docs updates (`PLANS.md`, `STATUS.md`, `DECISIONS.md`) for release traceability.
- [ ] Final verification checklist lock for V3 release.
