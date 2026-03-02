# PLANS.md — SatTrack 3D Roadmap

## Status
- Current Milestone: V1
- State: In Progress

## V1 — Core working feature
### Goal
Deliver a runnable single-file Cesium-based satellite tracker with live ISS + category satellites, interactive details, and side-panel controls.

### Done Means
- `index.html` opens and renders a 3D Cesium globe.
- Satellites render as moving entities with refresh every 10 seconds.
- ISS data and pass prediction are displayed.
- Search/filter/detail panel works.
- Orbit path visualization and user location marker are visible.

### Tasks
- [x] Define architecture and network decisions in `DECISIONS.md`.
- [x] Build single-file app UI + Cesium globe.
- [x] Integrate Open Notify ISS endpoint.
- [x] Integrate N2YO category satellites (via direct + proxy fallback).
- [x] Add category filtering, search, count, detail panel.
- [x] Add orbit path, day/night view, and user marker.
- [ ] Final V1 verification + milestone lock.

## V2 — Complete feature set
### Goal
Improve resiliency and UX quality.

### Tasks
- [ ] Add caching and smoother interpolation between updates.
- [ ] Add expanded satellite metadata cards.
- [ ] Improve error states and retries by endpoint.

## V3 — Production ready
### Goal
Harden deployment readiness.

### Tasks
- [ ] Optimize rendering settings + memory cleanup.
- [ ] Add smoke tests and accessibility pass.
- [ ] Final docs and release checklist.

## Risks & Mitigations
- Browser CORS limits against N2YO → use safe CORS proxy fallback.
- Third-party API rate limits → staggered refresh + concise dataset.
- Geolocation permission denial → graceful fallback text.
