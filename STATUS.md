# STATUS.md — Project Progress Tracker

Current Milestone: V1
Completed: Built SatTrack 3D single-file application with Cesium globe, live ISS + multi-category satellites, filters, search, details panel, orbit trails, day/night toggle, user marker, and ISS next pass estimate. Updated PLANS and DECISIONS for implementation traceability.
Verification: Build pass (static hosting), runtime smoke pass in headless browser, output runnable.
Next Step: Move to V2 enhancements (resiliency/performance) if requested.

## History
| # | Milestone | What Done | Build | Date |
|---|-----------|-----------|-------|------|
| 1 | V1 | Complete single-file SatTrack 3D implementation and docs updates | ✅ | 2026-03-02 |

## Active Assumptions
ASSUMPTION: Open Notify may intermittently reject browser-origin requests; N2YO ISS fallback remains available.
Reason: Public APIs can vary CORS/runtime availability.
Impact: ISS source may switch while preserving feature behavior.
Reversible: yes

ASSUMPTION: Category coverage is represented by curated, known NORAD IDs for Starlink/GPS/Weather.
Reason: SPEC asks for category filtering but does not define exact per-category count.
Impact: Deterministic tracked set with live telemetry.
Reversible: yes
