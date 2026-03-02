App Name: SatTrack 3D
Platform: Web (HTML + CSS + JavaScript, single file)
Goal: Professional 3D satellite tracking app with live data

Features:
- Real 3D Earth globe (CesiumJS)
- Live satellite positions updating every 10 seconds
- ISS live tracking (Open Notify API - no key needed)
- Multiple satellites from N2YO API
- Filter satellites by category (ISS, Starlink, GPS, Weather)
- Click satellite to see details (name, altitude, speed, lat/long)
- Orbit path visualization
- Day/Night Earth view
- Your location marker
- Next pass prediction for ISS
- Search satellite by name
- Satellite count display
- Clean modern UI panel on side

API Keys:
N2YO_API_KEY = "HMFZHK-PEFK9C-D4XXG8-5O6N"
CESIUM_ION_TOKEN = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI4YzM2MWNlOS1iOWE3LTRiMGEtYTVkYy1hZmFhYmQwNGFhZTQiLCJpZCI6Mzk2NTcwLCJpYXQiOjE3NzI0NDEzODJ9.6dJWQ2kBbeec8Yl8n9_rQ7FLmqv-QWgQgZqGrxV7PJY"

Technical:
- Single index.html file
- CesiumJS for 3D globe (CDN)
- Vanilla JavaScript
- No build step needed
- CORS proxy if needed for N2YO API

Network: ON
Allowed domains: api.n2yo.com, cesium.com, opennotify.org

Done Means:
User opens browser, sees 3D Earth with live satellites moving in real time, can filter and click satellites for info.

Create PLANS.md then build complete index.html.
Commit when done.
