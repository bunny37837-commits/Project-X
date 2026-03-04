# DECISIONS.md — SatTrack Pro Technical Decisions

## [DEC-001] Single-file production architecture
Date: 2026-03-02
Status: Decided

Decision: Implement the full product in one `index.html` with inline CSS and JavaScript.
Reason: SPEC requires single-file delivery with no local dependency installation.
Rejected: Multi-file or bundler-based setup.
Impact: Zero-build deployment and portable artifact.

## [DEC-002] 3D engine and imagery stack
Date: 2026-03-02
Status: Decided

Decision: Use CesiumJS (CDN) with Esri World Imagery as the base layer.
Reason: SPEC mandates Cesium and explicitly defines Esri imagery endpoint.
Rejected: Alternative map engines and imagery providers.
Impact: High-fidelity 3D globe with predictable tile source.

## [DEC-003] Telemetry source strategy (no API key)
Date: 2026-03-02
Status: Decided

Decision: Use only free, no-key sources from SPEC: Celestrak TLE (via corsproxy), Open Notify ISS, and OpenSky aircraft.
Reason: User and SPEC both require free/no-key runtime data paths.
Rejected: N2YO API-based enrichment.
Impact: Fully keyless runtime and cleaner compliance posture.

## [DEC-004] Performance controls
Date: 2026-03-02
Status: Decided

Decision: Cap satellites at 600, update propagation every 2 seconds, deduplicate entities in a map, and cache TLE for 1 hour in `localStorage`.
Reason: Direct alignment with SPEC performance section.
Rejected: Unbounded entity growth and no-cache fetch model.
Impact: Stable rendering behavior and reduced API/network churn.

## [DEC-005] Runtime resilience and UX safety
Date: 2026-03-02
Status: Decided

Decision: Add loading screen, toast-only error handling, and WebGL fallback panel while keeping sidebar/HUD available.
Reason: SPEC requires non-alert notifications and explicit fallback behavior.
Rejected: Browser alert flow and hard-crash initialization.
Impact: Better operational visibility and graceful degradation.
