# DECISIONS.md — SatTrack 3D Technical Decisions

## [DEC-001] Single-file architecture
Date: 2026-03-02
Status: Decided

Decision: Build the full app inside one `index.html` file with inline CSS and JavaScript.
Reason: SPEC explicitly requires no build step and single-file delivery.
Rejected: Multi-file bundling/toolchain, because it violates the constraint.
Impact: Simpler deployment and direct browser execution.

## [DEC-002] 3D engine selection
Date: 2026-03-02
Status: Decided

Decision: Use CesiumJS loaded from CDN with provided Cesium Ion token.
Reason: Required by SPEC for a real 3D globe and orbit visualization.
Rejected: Three.js custom globe; higher complexity and not requested.
Impact: High-fidelity Earth rendering and satellite entity support.

## [DEC-003] Satellite data strategy
Date: 2026-03-02
Status: Decided

Decision: Use Open Notify for ISS position and N2YO endpoints for additional satellites, refreshed every 10 seconds.
Reason: Aligns with live-data requirement and category support.
Rejected: Static mock satellite sets; would not meet “live” requirement.
Impact: App depends on external API responsiveness.

## [DEC-004] Network access policy
Date: 2026-03-02
Status: Decided

Decision: Network ON for runtime API calls.
Allowed Domains: `api.n2yo.com`, `api.wheretheiss.at`, `api.open-notify.org`, `cesium.com`, `unpkg.com`, `cors.isomorphic-git.org`
Reason: Required to fetch Cesium assets and live telemetry. Open Notify primary endpoint can be unavailable in browsers, so resilient fallbacks are included.

## [DEC-005] Security approach
Date: 2026-03-02
Status: Decided

Decision: Keep all requests read-only, avoid persistent credential storage, sanitize dynamic text with `textContent`.
Reason: Minimize XSS/credential risk in client-only app.
Rejected: HTML string injection for convenience.
Impact: Safer rendering and reduced exposure.
