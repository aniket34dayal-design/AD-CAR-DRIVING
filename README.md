# AD-CAR-DRIVING
A browser-based 3D arcade racing game set on Indian highways, built with React Three Fiber. Pick from 8 stylized Indian-inspired cars, dodge dense traffic across three lanes, and chain near-misses to rack up combo scores — all rendered in real time in the browser with no backend required.

Unsupported image
 
Unsupported image
 
Unsupported image
 
Unsupported image
 
Unsupported image

Features
8 stylized Indian cars — Maruti Swift Sport, Mahindra Thar 4x4, Tata Nano City, Wagon R, Hyundai Creta SX, Mahindra Scorpio-N, Maruti Alto K10, and Toyota Fortuner Legend. Each car has unique top speed, acceleration, handling, paint and silhouette.
3-lane Indian highway — scrolling asphalt with lane markings, palm trees, lamp posts, green highway signboards, colorful Indian-style hoardings, and lit roadside buildings.
4 weather / time-of-day modes — Bright Day, Mumbai Dusk, Bengaluru Night (with real headlights and lit billboards), and Monsoon (falling rain particles + fog).
Smart AI traffic — vehicles spawn ahead, take lanes, brake-light when slowing, and difficulty ramps up the further you drive.
Racing HUD — glowing speedometer (km/h matched to each car's top speed), distance, score, "Close Call" combo multiplier, neon warnings, and a pause menu.
Persistent high scores — best score and longest run saved to localStorage.
Pure frontend — no backend, no API keys, no accounts. Loads in a single browser tab.
Controls
Action	Keys
Steer left / right	A D or ← →
Accelerate	W or ↑
Brake	S, ↓, or Space
Pause / Resume	Esc
Tech Stack
React 19 + Vite 7 + TypeScript 5.9
three.js via @react-three/fiber and @react-three/drei
Tailwind CSS v4 with a custom dark racing theme (orange/yellow accents)
Custom lightweight game-state store using useSyncExternalStore
All 3D models built parametrically from primitives — no GLTF assets, no external downloads
Project Structure
artifacts/ad-car-simulator/
├── src/
│   ├── App.tsx              # Root, loads font and mounts <Game />
│   ├── index.css            # Theme tokens, glassmorphism, neon utilities
│   └── game/
│       ├── Game.tsx             # Main loop: input, physics, scoring, state machine
│       ├── Scene.tsx            # Three.js scene: camera follow, lights, weather, fog
│       ├── Road.tsx             # Scrolling road, lane lines, props, buildings, hoardings
│       ├── PlayerCar.tsx        # Player car with smooth lane interpolation + tilt
│       ├── Traffic.tsx          # AI traffic spawn / despawn / collision / near-miss
│       ├── CarModel.tsx         # Parametric 3D car (body, cabin, glass, wheels, lights)
│       ├── HUD.tsx              # Speedometer, score, combo, warnings, pause button
│       ├── MenuScreen.tsx       # Title / start screen
│       ├── CarSelectScreen.tsx  # Rotating 3D car showcase + weather picker
│       ├── PauseScreen.tsx      # Pause overlay
│       ├── GameOverScreen.tsx   # Crash summary + retry
│       ├── store.ts             # useSyncExternalStore-based game state store
│       └── types.ts             # CAR_MODELS catalog, lane positions, type defs
└── package.json

Getting Started
This artifact lives in a pnpm workspace monorepo. From the repo root:

# install
pnpm install
# run the game in dev mode
pnpm --filter @workspace/ad-car-simulator run dev
# typecheck
pnpm --filter @workspace/ad-car-simulator run typecheck
# production build
pnpm --filter @workspace/ad-car-simulator run build

The dev server reads its port from the PORT environment variable (default 21690).

How It Works
Game loop runs in a requestAnimationFrame tick that advances physics with a clamped delta. Speed, distance, score, and combo timers live in refs to avoid React re-renders.
Lanes are fixed at x = -3.2, 0, 3.2. The player car interpolates smoothly between lanes; AI traffic snaps and occasionally drifts.
Scoring is 1.5 × meters_traveled, plus a near-miss bonus of 50 × current_combo whenever you brush past a traffic car within ~1.4 m.
Difficulty ramps with distance, increasing traffic density and AI speed variance.
Collisions halt the run, persist any new high score, and surface the Game Over screen with stats.
Notes
This project uses parametric primitive geometry instead of any external 3D model files, so the entire game ships in a single small bundle and works offline once loaded.
Designed for desktop browsers with WebGL — keyboard input is required.
