Read AGENTS.md completely. Full production build — no shortcuts.

═══════════════════════════════════════════════════════════
APP NAME: SatTrack Pro
TAGLINE: "Real-time Earth Intelligence Platform"
FEEL: Palantir Gotham + NASA Mission Control + $80M product
FILE: Single index.html — all CSS + JS inline, no dependencies
═══════════════════════════════════════════════════════════

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DESIGN SYSTEM (FOLLOW EXACTLY)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

COLOR PALETTE:
  --bg-primary:     #050810   (near black, deep space)
  --bg-secondary:   #080d1a   (dark navy)
  --bg-panel:       #0a1628   (panel background)
  --bg-glass:       rgba(8, 16, 35, 0.85) (glassmorphism)
  --border-dim:     rgba(0, 212, 255, 0.08)
  --border-active:  rgba(0, 212, 255, 0.25)
  --accent-primary: #00d4ff   (electric cyan — primary)
  --accent-green:   #00ff88   (ISS / active)
  --accent-gold:    #ffd700   (ISS special)
  --accent-orange:  #ff6b35   (warnings)
  --accent-red:     #ff3355   (military / alerts)
  --text-primary:   #e8f4f8   (main text)
  --text-secondary: #7a9bb5   (muted text)
  --text-dim:       #3d5a6e   (very muted)
  --satellite-iss:      #ffd700
  --satellite-starlink: #00d4ff
  --satellite-gps:      #00ff88
  --satellite-weather:  #ff9500
  --satellite-military: #ff3355
  --satellite-other:    #8899aa

TYPOGRAPHY:
  Display font: 'Orbitron' (Google Fonts CDN) — headings, labels
  Body font: 'JetBrains Mono' (Google Fonts CDN) — data, values
  Import both from Google Fonts CDN in <head>

SPACING SYSTEM:
  Base unit: 4px
  Use: 4px, 8px, 12px, 16px, 24px, 32px only

BORDERS:
  All panels: 1px solid var(--border-dim)
  Active/hover: 1px solid var(--border-active)
  Border-radius: 2px (sharp, tactical feel — NOT rounded)

SHADOWS:
  Panel shadow: 0 4px 32px rgba(0,0,0,0.6)
  Glow effect: 0 0 20px rgba(0,212,255,0.15)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
LAYOUT ARCHITECTURE (PIXEL PRECISE)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Full viewport. No scroll. CSS Grid:

[TOP BAR          — 48px height, full width              ]
[LEFT SIDEBAR] [  CESIUM GLOBE — fills remaining space   ]
[ 280px wide ] [                                         ]
[             ] [  RIGHT PANEL — slides over globe       ]
[             ] [  320px, position absolute right        ]
[BOTTOM HUD       — 36px height, full width              ]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TOP BAR (48px — fixed)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Background: var(--bg-panel)
Border-bottom: 1px solid var(--border-dim)
Layout: flex, space-between, items-center, px-16

LEFT SECTION:
  - Logo: "⬡ SATTRACK PRO" in Orbitron font, 13px
    Color: var(--accent-primary)
    Letter-spacing: 3px
  - Separator: vertical line 1px, color: var(--border-active)
  - Status indicator: 
    Pulsing green dot (CSS animation, 2s ease infinite)
    Text: "LIVE" in JetBrains Mono, 10px, var(--accent-green)
    Letter-spacing: 2px

CENTER SECTION — MODE BUTTONS:
  4 buttons: [NORMAL] [NIGHT] [THERMAL] [CRT]
  Each button:
    Font: Orbitron 10px, letter-spacing 2px
    Padding: 6px 16px
    Border: 1px solid var(--border-dim)
    Background: transparent
    Color: var(--text-secondary)
    Border-radius: 2px
    Transition: all 0.2s ease
  
  Active state:
    Background: rgba(0,212,255,0.1)
    Border: 1px solid var(--accent-primary)
    Color: var(--accent-primary)
    Box-shadow: 0 0 12px rgba(0,212,255,0.2)
  
  Hover state:
    Background: rgba(0,212,255,0.05)
    Border: 1px solid rgba(0,212,255,0.3)

RIGHT SECTION:
  - UTC Clock: "UTC 14:23:07" JetBrains Mono 11px
    Updates every second via setInterval
    Color: var(--text-primary)
  - Separator
  - [REFRESH] button: same style as mode buttons
    Icon: "↻" + text "REFRESH"
  - [⊞] fullscreen toggle button

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
LEFT SIDEBAR (280px — fixed height, scrollable)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Background: var(--bg-glass)
Backdrop-filter: blur(12px)
Border-right: 1px solid var(--border-dim)
Overflow-y: auto
Custom scrollbar: 2px wide, color var(--border-active)
Padding: 12px

SECTION HEADERS style:
  Font: Orbitron 9px
  Letter-spacing: 3px
  Color: var(--text-dim)
  Text-transform: uppercase
  Padding: 8px 0 6px 0
  Border-bottom: 1px solid var(--border-dim)
  Margin-bottom: 8px

[SECTION: LAYERS]
  Toggle rows — each:
    Flex, space-between, align-center
    Padding: 8px 0
    Border-bottom: 1px solid rgba(255,255,255,0.03)
  
  Each layer row:
    Left: colored dot (4px circle) + layer name
    Right: custom toggle switch (CSS only)
    
  Layers:
    ● Satellites  [colored dot: --accent-primary]  [toggle]
    ● Aircraft    [colored dot: --accent-orange]   [toggle]
    ● ISS Track   [colored dot: --accent-gold]     [toggle]
    ● Orbits      [colored dot: --text-dim]        [toggle]

  Toggle switch CSS:
    Width: 32px, height: 16px
    Background when ON: var(--accent-primary)
    Background when OFF: var(--text-dim)
    Thumb: 12px white circle, transition 0.2s
    No JS needed for visual — use checkbox + label

[SECTION: FILTER]
  Category pills — wrap layout:
    [ALL] [ISS] [STARLINK] [GPS] [WEATHER] [MIL]
  
  Each pill:
    Font: JetBrains Mono 9px
    Padding: 3px 8px
    Border: 1px solid var(--border-dim)
    Border-radius: 2px
    Background: transparent
    Color: var(--text-secondary)
    Margin: 2px
    Cursor: pointer
  
  Active pill:
    Background: rgba(0,212,255,0.12)
    Border: 1px solid var(--accent-primary)
    Color: var(--accent-primary)

[SECTION: SEARCH]
  Input field:
    Width: 100%
    Background: rgba(0,0,0,0.4)
    Border: 1px solid var(--border-dim)
    Border-radius: 2px
    Color: var(--text-primary)
    Font: JetBrains Mono 11px
    Padding: 8px 10px
    Placeholder: "Search satellites..." color var(--text-dim)
  
  Focus state:
    Border: 1px solid var(--accent-primary)
    Box-shadow: 0 0 8px rgba(0,212,255,0.1)
    Outline: none

[SECTION: STATISTICS]
  2-column grid of stat cards:
  
  Each stat card:
    Background: rgba(0,0,0,0.3)
    Border: 1px solid var(--border-dim)
    Border-radius: 2px
    Padding: 8px
    Text-align: center
  
  Inside each card:
    Value: Orbitron 18px, var(--accent-primary)
    Label: JetBrains Mono 8px, var(--text-dim), letter-spacing 1px
  
  Cards:
    [SATELLITES: 847] [AIRCRAFT: 234]
    [COUNTRIES: 45 ] [ALTITUDE: 408km]

[SECTION: ISS TRACKER]
  Special highlighted box:
    Background: rgba(255, 215, 0, 0.05)
    Border: 1px solid rgba(255,215,0,0.2)
    Border-radius: 2px
    Padding: 12px
  
  Header: "● ISS" in gold with pulsing animation
  
  Data rows (JetBrains Mono 10px):
    LAT    28.614°N
    LON    77.209°E  
    ALT    408.3 km
    SPD    27,600 km/h
    PASS   14:23 UTC
  
  Each label: var(--text-dim), value: var(--text-primary)

[SECTION: SATELLITE LIST]
  Scrollable list of tracked satellites
  Max height: 200px, overflow-y scroll
  
  Each list item:
    Padding: 6px 8px
    Border-bottom: 1px solid rgba(255,255,255,0.03)
    Flex, align-center, gap 8px
    Cursor: pointer
  
  Inside:
    Colored dot (category color)
    Name: JetBrains Mono 10px, var(--text-primary)
    Alt: JetBrains Mono 9px, var(--text-dim)
  
  Hover: background rgba(0,212,255,0.05)
  Active/selected: background rgba(0,212,255,0.1),
    left border: 2px solid var(--accent-primary)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RIGHT DETAILS PANEL (320px — slides in/out)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Position: absolute, right: 0, top: 48px,
  bottom: 36px, width: 320px
Transform: translateX(100%) when closed
Transform: translateX(0) when open
Transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1)
Background: var(--bg-glass)
Backdrop-filter: blur(16px)
Border-left: 1px solid var(--border-dim)
Padding: 16px
Z-index: 100

CLOSE BUTTON:
  Position: top-right corner
  "✕" character, 14px, var(--text-secondary)
  Hover: var(--text-primary)

OBJECT TYPE BADGE:
  Small pill: "SATELLITE" or "AIRCRAFT"
  Font: Orbitron 8px, letter-spacing 2px
  Color based on type
  Border: 1px solid current color
  Padding: 2px 8px

OBJECT NAME:
  Font: Orbitron 16px
  Color: var(--text-primary)
  Margin: 8px 0

DIVIDER: 1px solid var(--border-dim)

DATA GRID (2 columns):
  Each cell:
    Label: JetBrains Mono 8px, var(--text-dim),
      letter-spacing 1px, uppercase
    Value: JetBrains Mono 13px, var(--text-primary)
    Padding: 8px 0
    Border-bottom: 1px solid rgba(255,255,255,0.03)
  
  For satellite:
    ALTITUDE     408.3 km
    SPEED        27,600 km/h
    LATITUDE     28.614°
    LONGITUDE    77.209°
    INCLINATION  51.6°
    PERIOD       92.7 min
    CATEGORY     ISS
    NORAD ID     25544
  
  For aircraft:
    CALLSIGN     AAI302
    ALTITUDE     10,668 m
    SPEED        890 km/h
    HEADING      045°
    ORIGIN       DEL
    DESTINATION  BOM
    SQUAWK       1234
    STATUS       AIRBORNE

ACTION BUTTONS (bottom of panel):
  [🎯 FLY TO]  [📍 TRACK]
  
  Each button:
    Flex 1, padding 10px
    Border: 1px solid var(--border-dim)
    Background: rgba(0,212,255,0.05)
    Color: var(--accent-primary)
    Font: Orbitron 9px, letter-spacing 2px
    Cursor: pointer
    Transition: all 0.2s
  
  Hover: 
    Background: rgba(0,212,255,0.15)
    Box-shadow: 0 0 16px rgba(0,212,255,0.2)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BOTTOM HUD BAR (36px — fixed)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Background: var(--bg-panel)
Border-top: 1px solid var(--border-dim)
Font: JetBrains Mono 10px, var(--text-secondary)
Flex, align-center, gap 24px, px 16px
Letter-spacing: 1px

Items (left to right):
  "LAT 00.000° N"  (updates on mouse move over globe)
  separator "|"
  "LON 00.000° E"
  separator "|"
  "ALT 408 KM"     (selected object altitude)
  separator "|"
  "SATS 847"       (live count)
  separator "|"
  "FPS 60"         (real FPS counter)
  separator "|"
  Right aligned: "LAST UPDATE 14:23:07"
  Pulsing red dot + "● LIVE"

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CESIUM GLOBE CONFIG
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Ion token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI4YzM2MWNlOS1iOWE3LTRiMGEtYTVkYy1hZmFhYmQwNGFhZTQiLCJpZCI6Mzk2NTcwLCJpYXQiOjE3NzI0NDEzODJ9.6dJWQ2kBbeec8Yl8n9_rQ7FLmqv-QWgQgZqGrxV7PJY

Viewer settings:
  animation: false
  baseLayerPicker: false
  geocoder: false
  homeButton: false
  infoBox: false
  sceneModePicker: false
  selectionIndicator: false
  timeline: false
  navigationHelpButton: false
  navigationInstructionsInitiallyVisible: false
  skyAtmosphere: new Cesium.SkyAtmosphere()
  globe.enableLighting: true
  scene.backgroundColor: Cesium.Color.BLACK

On globe mouse move:
  → Update LAT/LON in bottom HUD
  → Use scene.pick + globe.pick for coordinates

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DATA & SATELLITE LOGIC
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

TLE SOURCES (try in order):
1. https://corsproxy.io/?https://celestrak.org/NOAA/elements/gp.php?GROUP=active&FORMAT=tle
2. https://corsproxy.io/?https://celestrak.org/NOAA/elements/gp.php?GROUP=stations&FORMAT=tle

ISS LIVE:
  https://api.open-notify.org/iss-now.json
  Update every 5 seconds

AIRCRAFT:
  https://opensky-network.org/api/states/all
  Update every 15 seconds
  Handle 429 rate limit: show "(cached)" text in bottom HUD

SATELLITE CATEGORIES (assign by NORAD ID or name match):
  ISS: NORAD 25544 → gold color
  Starlink: name contains "STARLINK" → cyan
  GPS: name contains "GPS" or "NAVSTAR" → green
  Weather: name contains "NOAA","GOES","METEOSAT" → orange
  Military: name contains "USA-","NROL-","KH-" → red
  Other: everything else → dim grey

POSITION CALCULATION:
  Use satellite.js satrec + propagate()
  Update every satellite position every 2 seconds
  Show max 600 satellites simultaneously
  Orbit trail: store last 15 positions, draw as polyline
    Fading opacity from 0.8 (recent) to 0.1 (old)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
VISUAL MODES IMPLEMENTATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

NORMAL: no filter on #cesiumContainer

NIGHT VISION:
  CSS on #cesiumContainer:
    filter: brightness(1.2) contrast(1.4) 
            hue-rotate(90deg) saturate(2)
            sepia(0.3)
  Add scanline overlay div (::before pseudo):
    background: repeating-linear-gradient(
      0deg,
      rgba(0,0,0,0.03) 0px,
      rgba(0,0,0,0.03) 1px,
      transparent 1px,
      transparent 3px
    )
    pointer-events: none
    z-index: 50

THERMAL:
  CSS on #cesiumContainer:
    filter: sepia(1) hue-rotate(320deg) 
            saturate(5) brightness(0.9) contrast(1.3)

CRT:
  CSS on #cesiumContainer:
    filter: brightness(1.1) contrast(1.2) saturate(1.3)
  Add CRT overlay div:
    background: 
      repeating-linear-gradient(
        0deg,
        rgba(0,0,0,0.08) 0px,
        rgba(0,0,0,0.08) 1px,
        transparent 1px,
        transparent 2px
      )
    Add subtle RGB split: text-shadow on UI elements
    Add vignette: radial-gradient corners dark
    border-radius: 8px on cesium container
    box-shadow: inset 0 0 100px rgba(0,0,0,0.5)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ANIMATIONS & MICRO-INTERACTIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. LIVE DOT PULSE:
@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.4; transform: scale(0.8); }
}
animation: pulse 2s ease-in-out infinite

2. PANEL SLIDE:
  transition: transform 0.3s cubic-bezier(0.4,0,0.2,1)

3. DATA UPDATE FLASH:
  When ISS data updates:
    Brief flash: background rgba(0,212,255,0.15) → transparent
    Duration: 300ms

4. BUTTON HOVER GLOW:
  transition: all 0.2s ease
  box-shadow grows on hover

5. SATELLITE CLICK:
  Entity scale pulse animation in Cesium
  Right panel slides in simultaneously

6. LOADING STATE:
  On initial load: show centered loading screen
  "INITIALIZING SATTRACK PRO..." text
  Animated progress bar (CSS, not real progress)
  Font: Orbitron, color: var(--accent-primary)
  Hide after globe + first TLE fetch complete

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ERROR HANDLING (NO BROWSER ALERTS)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Create toast notification system:
  Position: top-right, below topbar
  Each toast:
    Background: var(--bg-panel)
    Border-left: 3px solid [color based on type]
    Padding: 10px 16px
    Font: JetBrains Mono 10px
    Auto-dismiss after 4 seconds
    Slide in from right, fade out

Toast types:
  ERROR: border var(--accent-red), icon "⚠"
  SUCCESS: border var(--accent-green), icon "✓"
  INFO: border var(--accent-primary), icon "ℹ"
  WARNING: border var(--accent-orange), icon "!"

Use for:
  - TLE fetch success/fail
  - Aircraft fetch rate limited
  - WebGL error
  - ISS position updated

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WEBGL FALLBACK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

If CesiumJS fails to initialize (WebGL error):
  Hide cesium container
  Show fallback panel:
    Background: var(--bg-secondary)
    Center: "WebGL Required" message
    Instructions for Chrome
    Still show sidebar with ISS data (fetch continues)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
KEYBOARD SHORTCUTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

N → NIGHT VISION mode
T → THERMAL mode
C → CRT mode
R → NORMAL mode + refresh
ESC → close right panel, deselect
F → fullscreen toggle
Space → pause/resume satellite updates

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PERFORMANCE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

- Max 600 satellite entities rendered at once
- Use requestAnimationFrame for FPS counter
- Batch Cesium entity updates (not one by one)
- Cache TLE data for 1 hour (localStorage)
- Satellite positions computed off main thread if possible
- Dedup: don't re-add entity if already exists, update position only
MAP IMAGERY (Add as Cesium base layer):
Use Esri World Imagery tiles — no key needed:
new Cesium.UrlTemplateImageryProvider({
  url: 'https://services.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}',
  credit: 'Esri World Imagery'
})
Add this as viewer's base imagery layer.

DATA SOURCES — ALL FREE, NO API KEY:
- TLE: https://corsproxy.io/?https://celestrak.org/NOAA/elements/gp.php?GROUP=active&FORMAT=tle
- ISS: https://api.open-notify.org/iss-now.json
- Aircraft: https://opensky-network.org/api/states/all
