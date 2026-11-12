# NET//BRAWL — Serverless P2P Network Traffic Side-Scroller

A self-contained single-file HTML5/Canvas side-scrolling battle game where **live webpage DOM structures** become jumpable platforms and **real post-page-load network requests** (`fetch`, `XMLHttpRequest`, and `PerformanceObserver` resource loads) dynamically spawn arena pickups, temporary bridges, shockwaves, and hazards.

## Features

- **DOM-to-Platform Engine:** Scans page elements (`<nav>`, `<article>`, `<section>`, `<aside>`, `[data-platform="true"]`) into a reachable 3-tier platform arena with one-way jump-through and drop-through mechanics.
- **Live Network Traffic Spawner:** Intercepts `window.fetch` and browser `PerformanceObserver` resource events in real time:
  - `GET / 200 OK`: Spawns **Data Packet Orbs** (`+15 HP`, `+30 Energy`).
  - `POST / PUT / DELETE`: Unleashes horizontal **Payload Shockwaves**.
  - `Heavy Resources (>3KB)`: Materializes temporary **Chunk Platforms**.
  - `4xx / 5xx Errors`: Fires vertical **HTTP 500 Laser Beams** with a telegraph warning phase.
- **Serverless WebRTC Peer-to-Peer (`RTCDataChannel`):** Connect two players over a LAN or static hosting (GitHub Pages, Netlify, Vercel) with zero backend servers using one-click **URL-hash invite links** (`#offer=...` and `#answer=...`) or manual SDP copy-paste.
- **4 ASCII Fighter Classes + Sprite Overlay:**
  - **NETRUNNER (`[O]`)**: Balanced stats; Special deploys a solid DOM Firewall platform and heals.
  - **DDoS JUGGERNAUT (`[###]`)**: High HP tank; Special fires a 3-way SYN Flood spread.
  - **0-DAY PHANTOM (`(o)`)**: High-speed glass cannon with double-jump; Special drops an `<XSS>` trap and blinks forward.
  - **WEB SPIDER (`/O\`)**: Arcing crawler projectiles; Special triggers a live `GET` request alongside a multi-bot Scrape Burst.
  - **Custom Sprite Overlay**: Upload any local PNG/GIF or paste an image URL to render a scaled sprite directly over your character's ASCII hitbox.
- **Web Audio API Synthesizer:** Warm, low-pass filtered procedural sound effects for jumps, attacks, specials, packet pickups, and error alarms (toggleable via `SFX: ON/OFF`).
- **Stuck-Free AI Opponent:** Built-in bot navigates multi-tier platforms, drops through ledges when pursuing below, and climbs adjacent tiers when pursuing above.

## Quick Start

1. Download `index.html`.
2. Open `index.html` directly in any modern browser (Chrome, Firefox, Edge, Safari) or serve it locally:
   ```bash
   python3 -m http.server 8000
   ```
3. Play immediately against the AI bot, or click **P2P Connect** to invite another player.

## Controls

| Action | Keys |
| :--- | :--- |
| **Move Left / Right** | `A` / `D` or `Left` / `Right` Arrow |
| **Jump (Double-Jump for Phantom)** | `W` or `Up` Arrow |
| **Drop Through Platform** | `S` or `Down` Arrow |
| **Primary Attack** | `Space`, `Z`, or `J` |
| **Class Special Ability** | `X`, `K`, or `Shift` |

## Peer-to-Peer Multiplayer Setup (LAN & Static Sites)

1. **Host (Player 1):** Click **P2P Connect** -> **1. Generate Invite Link** -> **Copy Box**, and send the `#offer=...` URL to Player 2.
2. **Joiner (Player 2):** Open the invite link. The page automatically processes the offer and generates a `#answer=...` URL. Copy and send that link back to Player 1.
3. **Host (Player 1):** Open the `#answer=...` link (or paste the code into the P2P modal and click **Finalize**). The status badge turns green (`P2P: CONNECTED`) once the direct `RTCDataChannel` opens.

## Deploying to GitHub Pages / Netlify

Because the entire game lives inside a single `index.html` file with zero external dependencies, upload `index.html` to any static host (GitHub Pages, Netlify, Cloudflare Pages, or an S3 bucket). Public STUN (`stun:stun.l.google.com:19302`) is preconfigured for NAT traversal across the internet.
